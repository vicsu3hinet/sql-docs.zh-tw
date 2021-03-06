---
title: "sys.resource_stats （SQL Azure 資料庫） |Microsoft 文件"
ms.custom: 
ms.date: 05/23/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72b0dc0c526198dc49047f44be0cce47ea7f3455
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 Azure SQL Database 的 CPU 使用量和儲存體資料。 於五分鐘間隔內收集及彙總資料。 每個使用者資料庫各有一個資料列代表每隔五分鐘報告資源耗用變化的視窗。 其中包括 CPU 使用率、儲存體大小或資料庫 SKU 修改。 沒有變更的閒置資料庫則不會每五鐘顯示資料列。 歷程記錄資料大約會保留 14 天。  
  
 **Sys.resource_stats**檢視具有不同的定義，根據資料庫相關聯的 Azure SQL Database 伺服器的版本。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。  
  
 下表描述 v12 伺服器中可用的資料行：  
  
|資料行 (v12 server)|資料類型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 時間，表示 5 分鐘報告間隔的開始。|  
|end_time|**datetime**|UTC 時間表示 5 分鐘報告間隔的結束。|  
|database_name|**varchar**|使用者資料庫的名稱。|  
|sku|**varchar**|資料庫服務層。 以下是可能的值：<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|storage_in_megabytes|**float**|時間週期內的最大儲存體大小 (MB)，其中包括資料庫資料、索引、預存程序和中繼資料。|  
|avg_cpu_percent|**numeric**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**numeric**|根據服務層限制，計算平均 I/O 使用率的百分比。|  
|avg_log_write_percent|**numeric**|平均寫入資源使用率，以服務層限制的百分比計算。|  
|max_worker_percent|**decimal(5,2)**|最大並行工作者 （要求），以根據資料庫的服務層限制的百分比表示。<br /><br /> 最大值目前計算 5 分鐘的間隔 15 的第二個樣本的並行工作者計數為基礎。|  
|max_session_percent|**decimal(5,2)**|以百分比表示，根據資料庫的服務層限制的最大並行工作階段。<br /><br /> 最大值目前計算 5 分鐘的間隔 15 的第二個樣本的並行工作階段計數為基礎。|  
|dtu_limit|**int**|目前最大資料庫 DTU 此資料庫設定此間隔。|  
  
> [!TIP]  
>  詳細說明這些限制，以及服務層的內容，請參閱主題[服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[服務層的功能以及限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)。  
  
 下表描述 v11 伺服器中可用的資料行：  
  
|資料行 (v11 server)|資料類型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 時間，表示 5 分鐘報告間隔的開始。|  
|end_time|**datetime**|UTC 時間表示 5 分鐘報告間隔的結束。|  
|database_name|**nvarchar**|資料庫的名稱。|  
|sku|**nvarchar**|資料庫服務層。 以下是可能的值：<br /><br /> Web<br /><br /> Business<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|*注意： V11 這個資料行已被取代，其值永遠為 0。*<br /><br /> 自上次度量以來所使用的 CPU 時間。<br /><br /> 對於 CPU 度量，我們建議您改用**avg_cpu_cores_used**資料行，而不是此資料行。|  
|storage_in_megabytes|**decimal**|時間週期內的最大儲存體大小 (MB)，其中包括資料庫資料、索引、預存程序和中繼資料。|  
|avg_cpu_cores_used|**decimal**|*注意： V11 這個資料行已被取代，其值永遠為 0。*<br /><br /> 此時間間隔中使用的平均 CPU 核心數。|  
|avg_physical_read_iops|**decimal**|*注意： V11 這個資料行已被取代，其值永遠為 0。*<br /><br /> 此時間間隔中平均讀取的 IOPS。|  
|avg_physical_write_iops|**decimal**|*注意： V11 這個資料行已被取代，其值永遠為 0。*<br /><br /> 此時間間隔中平均寫入的 IOPS。|  
|active_memory_used_kb|**bigint**|*注意： V11 這個資料行已被取代，其值永遠為 0。*<br /><br /> 在此時間間隔結束時，正在使用的作用中記憶體計數。|  
|active_session_count|**int**|在此時間間隔結束時的作用中工作階段計數。|  
|active_worker_count|**int**|在此時間間隔結束時的作用中工作者計數。|  
|avg_cpu_percent|**decimal**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_physical_data_read_percent|**decimal**|根據服務層限制，計算平均 I/O 使用率的百分比。|  
|avg_log_write_percent|**decimal**|平均寫入資源使用率，以服務層限制的百分比計算。|  
  
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.resource_stats**的最大允許您正在為 Basic、 Standard 和 Premium 資料庫的服務層/效能層級的 DTU 限制百分比表示。  若為 Web 與 Business 層，則這些數字表示 Standard S2 執行層的百分比。  例如，對 Web 資料庫執行時，若 avg_cpu_percent 傳回 70%，則表示 S2 層限制的 70%。 此外，若為 Web 和 Business 層，則百分比可能會反映超過 100% 的數字，這也是依據 S2 層的限制。  
  
 彈性集區的成員資料庫時，資源統計資料呈現為百分比值，會在彈性集區設定中所設定的資料庫最大 DTU 限制百分比表示。  
  
 這項資料的更細微的檢視，使用**sys.dm_db_resource_stats**使用者資料庫中的動態管理檢視。 此檢視表每隔 15 秒就會擷取一次資料，並會維持 1 小時內的歷程記錄資料。  如需詳細資訊，請參閱[sys.dm_db_resource_stats &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>範例  
 下列範例會傳回上一週平均至少為 80% 運算使用率的所有資料庫。  
  
```  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
  
 以下範例會計算指定之資料庫的平均 DTU 耗用百分比。 (此查詢只適用於針對 v11 伺服器執行。)  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
   FROM (VALUES (avg_cpu_percent), (avg_physical_data_read_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.resource_stats   
WHERE database_name = '<your db name>'   
ORDER BY end_time DESC;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層的功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
