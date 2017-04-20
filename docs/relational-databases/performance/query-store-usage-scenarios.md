---
title: "查詢存放區使用案例 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/12/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-query-tuning"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查詢存放區, 使用案例"
ms.assetid: f5309285-ce93-472c-944b-9014dc8f001d
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# 查詢存放區使用案例
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  若追蹤並確保可預測的工作負載效能非常重要，就能在整組案例中廣泛使用查詢存放區。 以下是您可以考慮的一些範例︰  
  
-   透過計畫選擇迴歸找出並修正查詢  
  
-   找出並調整熱門資源取用查詢  
  
-   A/B 測試  
  
-   在升級到 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
-   找出並改善特定的工作負載  
  
## 透過計畫選擇迴歸找出並修正查詢  
 在一般查詢執行期間，查詢最佳化工具可能會決定採取不同的計畫，因為重要的輸入已改變：資料基數已變更；建立、變更或卸除索引；統計資料已更新等。在大多數情況下，比起先前使用的計畫，其挑選的新計畫會更好或不相上下。 不過，還是會出現新計畫明顯比較糟糕的情況，而我們將這類情況稱為計畫選擇變更迴歸。 在查詢存放區之前，很難找出並修正問題，因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並未提供內建資料存放區，讓使用者可查看某一段時間內所使用的執行計畫。  
  
 現在，透過查詢存放區，您可以快速地：  
  
-   識別已在感興趣的時段 (過去 1 小時、天、週等) 中將執行計量降級的所有查詢。 使用 **中的** 迴歸查詢 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來加速您的分析。  
  
-   在迴歸查詢之間，很容易就能找出具有多個計畫的查詢，以及因為不正確的計畫選擇而遭到降級的查詢。 使用 [迴歸查詢]  中的 [計畫摘要]  窗格，以視覺化方式顯示某個迴歸查詢的所有計畫及其在某一段期間內的查詢效能。  
  
-   從歷程記錄中強制執行先前的計畫 (如果已證實該計畫比較好)。 使用 [迴歸查詢]  中的 [強制計畫]  按鈕，強制執行針對查詢所選取的計畫。  
  
 ![query-store-usage-1](../../relational-databases/performance/media/query-store-usage-1.png "query-store-usage-1")  
  
 如需此案例的詳細說明，請參閱 [查詢存放區︰適用於資料庫的飛行資料記錄器](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/) 部落格。  
  
## 找出並調整熱門資源取用查詢  
 雖然您的工作負載可能會產生成千上萬個查詢，但通常只有其中幾個實際上最常使用系統資源，因而需要您多加注意。 在熱門資源取用查詢中，您通常會發現這類查詢若不是迴歸的，就是可以透過其他調整來改善的查詢。  
  
 開始探勘的最簡單方式是開啟 **中的 [熱門資源取用查詢]**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。  使用者介面會分成三個窗格︰代表熱門資源取用查詢的長條圖 (左)、所選取查詢的計畫摘要 (右)，以及所選取計畫的視覺化查詢計畫 (下方)。 按一下 [設定]  按鈕，來控制您想要分析的查詢數量以及感興趣的時間間隔。 此外，您可以在不同的資源耗用維度 (持續時間、CPU、記憶體、IO、執行數目) 和基準 (平均、最小值、最大值、總計、標準差) 之間進行選擇。  
  
 ![query-store-usage-2](../../relational-databases/performance/media/query-store-usage-2.png "query-store-usage-2")  
  
 查看右邊的計畫摘要來分析執行歷程記錄，並了解不同的計畫及其執行階段統計資料。 使用下方窗格來檢查不同的計畫，或是以視覺化的並排顯示方式來比較它們 (使用 [比較] 按鈕)。  
  
 當您識別效能次佳的查詢時，您的動作取決於問題的本質：  
  
1.  如果是以多個計畫來執行查詢，且最後一個計畫明顯比前一個計畫差，則您可以使用計畫強制執行機制，以確保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 將一律使用最佳計畫來進行未來的執行。  
  
2.  檢查最佳化工具是否在 XML 計畫中建議任何遺漏的索引。 如果是，請建立遺漏的索引，並使用查詢存放區來評估索引建立之後的查詢效能  
  
3.  確定針對查詢所使用之基礎資料表的統計資料是最新的。  
  
4.  確定查詢所使用的索引會重組。  
  
5.  考慮重寫耗用資源的查詢。 例如，充分利用查詢參數化並減少動態 SQL 的使用。 在讀取資料時實作最佳邏輯 (在資料庫端套用資料篩選，而不是在應用程式端)。  
  
## A/B 測試  
 使用查詢存放區，來比較您計畫引進之應用程式變更前後的工作負載效能。  下列清單包含數個範例，您可以使用查詢存放區，來評估環境或應用程式變更對工作負載效能的影響︰  
  
-   推出新的應用程式版本。  
  
-   在伺服器上新增硬體。  
  
-   在資料表上建立耗用資源之查詢所參考的遺漏索引。  
  
-   套用安全性原則以取得資料列層級安全性。 如需詳細資訊，請參閱 [使用查詢存放區最佳化資料列層級安全性](http://blogs.msdn.com/b/sqlsecurity/archive/2015/07/21/optimizing-rls-performance-with-the-query-store.aspx)。  
  
-   將暫時性系統版本設定新增到您 OLTP 應用程式經常修改的資料表中。  
  
 在上述任何案例中，套用下列工作流程︰  
  
1.  在計畫的變更之前使用查詢存放區來執行您的工作負載，以產生效能基準。  
  
2.  在目前受控制的時段中套用應用程式變更。  
  
3.  繼續執行工作負載一段足夠的時間，才能產生變更之後的系統效能影像  
  
4.  比較 #1 和 #3 的結果。  
  
    1.  開啟 [整體資料庫耗用量]  來判斷對整個資料庫的影響  
  
    2.  開啟 [資源耗用量排名在前的查詢] (或使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 執行您自己的分析)，以分析變更最重要的查詢的影響。  
  
5.  萬一無法接受新的效能，請決定要保留變更，或是執行復原。  
  
 下圖顯示發生遺漏索引建立情況的查詢存放區分析 (步驟 4)。 開啟 [熱門資源取用查詢] / [計畫摘要] 窗格，即可針對應該會受到索引建立影響的查詢取得這個檢視︰  
  
 ![query-store-usage-3](../../relational-databases/performance/media/query-store-usage-3.png "query-store-usage-3")  
  
 此外，您可以將計畫在索引建立前後的情況並排顯示以進行比較 (「在另一個視窗中比較所選查詢的計畫」工具列選項，在工具列上會以紅色方塊標示)。  
  
 ![query-store-usage-4](../../relational-databases/performance/media/query-store-usage-4.png "query-store-usage-4")  
  
 索引建立之前的計畫 (plan_id  = 1，上方) 具有遺漏索引提示，而您可以檢查叢集索引掃描是查詢中最耗用資源的運算子 (紅色矩形)。  
  
 遺漏索引建立之後的計畫 (plan_id = 15，下方) 現在具有索引搜尋 (非叢集的)，可降低查詢的整體成本並提升其效能 (綠色矩形)。  
  
 根據分析，您很可能會保留索引，因為查詢效能已改善。  
  
## 在升級到 SQL Server 2016 期間保持效能穩定性  
 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]之前，使用者在升級到最新平台版本期間，會暴露在效能衰退的風險中。 原因在於，最新版的查詢最佳化工具會在安裝新的位元之後立即變成使用中狀態。  
  
 從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 開始，所有的查詢最佳化工具變更都會繫結至最新的 `COMPATIBILITY_LEVEL`，因此，計畫在升級時不會立即變更，而是在使用者將 `COMPATIBILITY_LEVEL` 變更為最新版本時變更。 此功能會結合查詢存放區，可讓您在升級過程中對查詢效能擁有絕佳層級的控制。 下圖顯示建議的升級工作流程：  
  
 ![query-store-usage-5](../../relational-databases/performance/media/query-store-usage-5.png "query-store-usage-5")  
  
1.  升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 而不需要變更 `COMPATIBILITY_LEVEL`。 它不會為您公開最新的查詢最佳化工具，但可為您提供 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 功能 (包括查詢存放區)。  
  
2.  啟用查詢存放區︰擷取查詢和計畫，並利用先前的 `COMPATIBILITY_LEVEL`來建立效能基準。 在這個步驟中保持足夠的時間，以擷取所有的計畫並取得穩定的基準。  
  
3.  移至最新的相容性層級︰將您的工作負載公開至最新的查詢最佳化工具，並讓它建立潛在的新計畫。  
  
4.  使用查詢存放區進行分析和迴歸修正︰在大多數情況下，新的查詢最佳化工具應該會產生更好的計畫。 不過，查詢存放區可讓您輕鬆找出計畫選擇迴歸，並使用計畫強制執行機制加以修正。  
  
## 找出並改善特定的工作負載  
 某些工作負載沒有主控查詢，可讓您加以調整來改善整體應用程式效能。 這些工作負載通常是使用相對大量的各種查詢做為特性，這其中每一個查詢都會耗用部分的系統資源。 由於是唯一的，這些查詢很少執行 (通常只執行一次，因此會以特別的方式命名)，所以它們的執行階段耗用量並不重要。 相反地，假設該應用程式會不停地產生全新的查詢，則會在不是最佳化的查詢編譯中耗費絕大部分的系統資源。 這對查詢存放區而言不是理想的情況，假設有更大量的查詢和計畫湧進您所保留的空間，這表示查詢存放區很可能會非常快速地以唯讀模式結束。 若您啟用 [Size Based Cleanup Policy (大小基礎清除原則)] ([強烈建議](https://msdn.microsoft.com/library/mt604821.aspx)持續啟動並執行查詢存放區)，則背景處理程序大部分的時間將會清除查詢存放區結構，並佔用大量系統資源。  
  
 [資源耗用量排名在前的查詢] 檢視會提供您的工作負載的特定本質的初步指示：  
  
 ![query-store-usage-6](../../relational-databases/performance/media/query-store-usage-6.png "query-store-usage-6")  
  
 使用 [執行計數] 計量來分析您排名最前面的查詢是否是特定的 (這需要您使用 `QUERY_CAPTURE_MODE = ALL` 來執行查詢存放區)。 您可以從上圖看見 90% 的 **熱門資源取用查詢** 只會執行一次。  
  
 或者，您可以執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼來取得系統中查詢文字、查詢計畫的總數，並透過比較其 query_hash 和 plan_hash，進而判斷它們之間的差異：  
  
```  
/*Do cardinality analysis when suspect on ad-hoc workloads*/  
SELECT COUNT(*) AS CountQueryTextRows FROM sys.query_store_query_text;  
SELECT COUNT(*) AS CountQueryRows FROM sys.query_store_query;  
SELECT COUNT(DISTINCT query_hash) AS CountDifferentQueryRows FROM  sys.query_store_query;  
SELECT COUNT(*) AS CountPlanRows FROM sys.query_store_plan;  
SELECT COUNT(DISTINCT query_plan_hash) AS  CountDifferentPlanRows FROM  sys.query_store_plan;  
```  
  
 這是您在使用特定查詢產生工作負載的情況下一個可能得到的結果：  
  
 ![query-store-usage-7](../../relational-databases/performance/media/query-store-usage-7.png "query-store-usage-7")  
  
 查詢結果顯示，儘管查詢存放區中有大量的查詢和計畫，但它們的 query_hash 和 plan_hash 實際上是一樣的。 唯一的查詢文字和唯一 query_hash 之間的比率遠大於 1，這個比率指出當查詢之間唯一的差異是提供來做為查詢文字一部分的常值常數 (參數) 時，工作負載是適合用來參數化的候選項目。  
  
 如果您的應用程式會產生查詢 (而不是叫用預存程序或參數化查詢)，或者它依賴預設會產生查詢的物件關聯式對應架構，通常就會發生這種狀況。  
  
 如果您可以控制應用程式程式碼，您或許就能考慮重新撰寫資料存取層來利用預存程序或參數化查詢。 不過，這種情況也會大幅改善，而不需要藉由針對整個資料庫 (所有查詢) 或含有相同 query_hash 的個別查詢範本強制執行查詢參數化來進行應用程式變更。  
  
 使用個別查詢範本的方法需要建立計畫指南︰  
  
```  
  
/*Apply plan guide for the selected query template*/  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'<your query text goes here>',  
    @stmt OUTPUT,   
    @params OUTPUT;  
  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION (PARAMETERIZATION FORCED)';  
```  
  
 含有計畫指南的解決方案來得更精確，但需要更多工作。  
  
 如果您的所有查詢 (或大部分查詢) 是適用於自動參數化的候選項目，則針對整個資料庫變更 `FORCED PARAMETERIZATION` 可能就是更好的選項：  
  
```  
  
/*Apply forced parameterization for entire database*/  
ALTER DATABASE <database name> SET PARAMETERIZATION  FORCED;  
```  
  
 在您套用這其中任何步驟之後， **熱門資源取用查詢** 將會針對您的工作負載顯示不同的圖片。  
  
 ![query-store-usage-8](../../relational-databases/performance/media/query-store-usage-8.png "query-store-usage-8")  
  
 在某些情況下，您的應用程式可能會產生許多各種不適合用來做為自動參數化候選項目的查詢。 在此情況下，您將會在系統中看到大量查詢，但在唯一查詢與唯一 query_hash 之間的比率很可能會接近 1。  
  
 在此情況下，您可能想要設定 'optimize for ad hoc workloads'，以避免在可能不會再次執行的查詢上浪費快取記憶體。 若要避免在查詢存放區中擷取這些查詢，請將 `QUERY_CAPTURE_MODE` 設為 `AUTO`。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
  
sp_configure 'optimize for ad hoc workloads', 1;  
GO  
RECONFIGURE;  
GO  
  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE CLEAR;  
ALTER DATABASE  [QueryStoreTest] SET QUERY_STORE = ON   
    (OPERATION_MODE = READ_WRITE, QUERY_CAPTURE_MODE = AUTO);  
```  
  
## 另請參閱  
 [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)   
 [使用查詢存放區的最佳作法](../../relational-databases/performance/best-practice-with-the-query-store.md)  
  
  