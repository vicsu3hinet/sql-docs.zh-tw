---
title: "解決記憶體不足問題 | Microsoft Docs"
ms.custom: ""
ms.date: "08/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: 18
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 18
---
# 解決記憶體不足問題
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 所使用的記憶體比 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更多，而且使用方式也不同。 您所安裝並配置給 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 的記憶體數量可能會變得不足以支應成長的需求。 若是如此，您可能會用完記憶體。 本主題將說明如何從 OOM 情況中復原。 如需可協助您避免多種 OOM 情況的指引，請參閱[監視與疑難排解記憶體使用量](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)。  
  
## 本主題所涵蓋的內容  
  
|主題|概觀|  
|-----------|--------------|  
|[解決由於 OOM 所造成的資料庫還原失敗](../../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md#bkmk_resolveRecoveryFailures)|如果您收到錯誤訊息：「資料庫 '*\<資料庫名稱>*' 的還原作業因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足而失敗」，該怎麼辦。|  
|[解決低記憶體或 OOM 狀況對於工作負載的影響](../../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md#bkmk_recoverFromOOM)|如果您發現低記憶體問題對於效能造成負面影響，該怎麼辦。|  
|[解決有足夠的記憶體可用但卻記憶體不足所造成的頁面配置失敗](../../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md#bkmk_PageAllocFailure)|如果您收到錯誤訊息：「不允許資料庫 '*\<資料庫名稱>*' 的頁面配置，因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足」，該怎麼辦。 …” 前提是可用的記憶體足夠供執行作業。|  
  
##  <a name="bkmk_resolveRecoveryFailures"></a> 解決由於 OOM 所造成的資料庫還原失敗  
 當您嘗試還原資料庫時，可能會收到錯誤訊息：「資料庫 '*\<資料庫名稱>*' 的還原作業因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足而失敗」。這表示伺服器沒有足夠的可用記憶體來還原資料庫。
   
您還原資料庫的目標伺服器針對資料庫備份的記憶體最佳化資料表必須有足夠的可用記憶體，否則資料庫將不會恢復連線。  
  
如果伺服器確實有足夠的實體記憶體，但您仍發現此錯誤，可能是其他處理序使用太多記憶體，或組態問題導致沒有足夠的記憶體可供還原使用。 針對這類問題，請採取下列措施將更多記憶體提供給還原作業： 
  
-   暫時關閉執行中的應用程式。   
    透過關閉一個或多個執行中的應用程式或停止目前不需要的服務，就可以將這些應用程式或服務所使用的記憶體提供給還原作業。 您可以在成功還原之後重新啟動這些應用程式。  
  
-   提高 MAX_MEMORY_PERCENT 的值。   
    如果資料庫已[繫結至資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) (這是最佳做法)，還原作業可用的記憶體是由 MAX_MEMORY_PERCENT 所管理。 如果此值太低，還原就會失敗。 這個程式碼片段會將資源集區 PoolHk 的 MAX_MEMORY_PERCENT 變更為已安裝記憶體的 70%。  
  
    > [!IMPORTANT]  
    >  如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 設成與 MAX_MEMORY_PERCENT 相同的值。   
    > 如需詳細資訊，請參閱[最佳做法：在 VM 環境使用記憶體內部 OLTP](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md) 主題。  
  
    ```tsql  
  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     如需 MAX_MEMORY_PERCENT 之最大值的資訊，請參閱主題章節：[可用於記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
-   增加**最大伺服器記憶體**。  
    如需設定 [最大伺服器記憶體] 的資訊，請參閱[使用記憶體組態選項最佳化伺服器效能](http://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx)主題。  
  
##  <a name="bkmk_recoverFromOOM"></a> 解決低記憶體或 OOM 狀況對於工作負載的影響  
 避免發生低記憶體或 OOM (記憶體不足) 的情況才是最上策。 良好的規劃和監視有助於避免 OOM 情況。 不過，最佳的規劃永遠無法預測實際發生的狀況，而最後可能會導致低記憶體或 OOM。 有兩個步驟可以從 OOM 中復原：  
  
1.  [開啟 DAC (專用管理員連接)](../../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md#bkmk_openDAC)  
  
2.  [採取更正動作](../../relational-databases/in-memory-oltp/resolve-out-of-memory-issues.md#bkmk_takeCorrectiveAction)  
  
###  <a name="bkmk_openDAC"></a> 開啟 DAC (專用管理員連接)  
 Microsoft SQL Server 提供了專用管理員連接 (DAC)。 即使伺服器對其他用戶端連接沒有回應，系統管理員也可以使用 DAC 來存取 SQL Server Database Engine 的執行中執行個體，以針對伺服器上的問題進行疑難排解。 您可以透過 `sqlcmd` 公用程式和 SQL Server Management Studio (SSMS) 使用 DAC。  
  
 如需使用 `sqlcmd` 和 DAC 的指引，請參閱[使用專用管理員連接](http://msdn.microsoft.com/library/ms189595\(v=sql.100\).aspx/css)。 如需透過 SSMS 使用 DAC 的指引，請參閱[如何：利用 SQL Server Management Studio 使用專用管理員連接](http://msdn.microsoft.com/library/ms178068.aspx)。  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 採取更正動作  
 若要解決 OOM 狀況，您必須透過降低使用量，釋出現有的記憶體，或是將更多記憶體提供給記憶體中的資料表。  
  
#### 釋出現有的記憶體  
  
##### 刪除非必要的記憶體最佳化資料表資料列並等候記憶體回收  
 您可以從記憶體最佳化資料表中移除非必要的資料列。 記憶體回收行程會將這些資料列所使用的記憶體傳回給可用的記憶體。 。 記憶體中 OLTP 引擎會積極地回收資料列佔用的記憶體。 不過，長時間執行的交易可能會防止記憶體回收。 例如，假設您的交易會執行 5 分鐘，則任何在交易作用期間由於更新/刪除作業而建立的資料列版本，都無法進行記憶體回收。  
  
##### 將一個或多個資料列移至磁碟資料表  
 下列 TechNet 文件提供了有關將記憶體最佳化資料表的資料列移至磁碟資料表的指引。  
  
-   [應用程式層級資料分割](http://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [分割記憶體最佳化資料表的應用程式模式](http://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### 增加可用的記憶體  
  
##### 提高資源集區的 MAX_MEMORY_PERCENT 值  
 如果您尚未針對記憶體中的資料表建立具名資源集區，就應該先建立集區，並且將 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫繫結至該集區。 如需如何建立 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫並繫結至資源集區的指引，請參閱[將包含記憶體最佳化資料表的資料庫繫結至資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)主題。  
  
 如果您的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 資料庫已繫結至資源集區，您應該能夠提高集區可存取的記憶體百分比。 如需變更資源集區之 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT 值的指引，請參閱[變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 子主題。  
  
 提高 MAX_MEMORY_PERCENT 的值。   
這個程式碼片段會將資源集區 PoolHk 的 MAX_MEMORY_PERCENT 變更為已安裝記憶體的 70%。  
  
> [!IMPORTANT]  
>  如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 與 MAX_MEMORY_PERCENT 設為相同值。   
> 如需詳細資訊，請參閱[最佳做法：在 VM 環境使用記憶體內部 OLTP](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md) 主題。  
  
```tsql  
  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor  
--    RECONFIGURE enables resource governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
  
```  
  
 如需 MAX_MEMORY_PERCENT 之最大值的資訊，請參閱主題章節：[可用於記憶體最佳化資料表和索引的記憶體百分比](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)。  
  
##### 安裝額外記憶體  
 最佳的終極解決方案還是安裝額外的實體記憶體 (如果可行)。 如果您這樣做，請記住，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不太可能需要更多記憶體，所以您或許能夠一併提高 MAX_MEMORY_PERCENT 的值 (請參閱[變更現有集區上的 MIN_MEMORY_PERCENT 和 MAX_MEMORY_PERCENT](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 子主題)，以便將大部分新安裝的記憶體提供給資源集區。  
  
> [!IMPORTANT]  
>  如果伺服器是在 VM 上執行，而且不是專用的，請將 MIN_MEMORY_PERCENT 與 MAX_MEMORY_PERCENT 設為相同值。   
> 如需詳細資訊，請參閱[最佳做法：在 VM 環境使用記憶體內部 OLTP](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md) 主題。  
  
##  <a name="bkmk_PageAllocFailure"></a> 解決有足夠的記憶體可用但卻記憶體不足所造成的頁面配置失敗  
 如果您收到錯誤訊息：「不允許資料庫 '*\<資料庫名稱>*' 的頁面配置，因為資源集區 '*\<資源集區名稱>*' 中的記憶體不足」。 如需詳細資訊，請參閱 'http://go.microsoft.com/fwlink/?LinkId=330673'。 在錯誤記錄檔中，可用的實體記憶體已足夠配置頁面時，它可能是因為已停用的資源管理員。 若資源管理員已停用，MEMORYBROKER_FOR_RESERVE 會誘發不實的記憶體壓力。  
  
 為了解決此問題，您必須啟用資源管理員。  
  
 如需使用物件總管、資源管理員屬性或 Transact-SQL 來啟用資源管理員之限制事項的資訊和指引，請參閱[啟用資源管理員](http://technet.microsoft.com/library/bb895149.aspx)。  
  
## 另請參閱  
 [為記憶體中的 OLTP 管理記憶體](../Topic/Managing%20Memory%20for%20In-Memory%20OLTP.md)   
 [監視與疑難排解記憶體使用量](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [將包含記憶體最佳化資料表的資料庫繫結至資源集區](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [最佳作法：在 VM 環境使用記憶體中 OLTP](../Topic/Using%20In-Memory%20OLTP%20in%20a%20VM%20Environment.md)  
  
  