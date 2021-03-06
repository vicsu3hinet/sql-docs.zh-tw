---
title: "監視應用裝置健全狀況狀態 (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 91132e3c-3137-4670-adaa-8a7b234fb8d2
caps.latest.revision: "12"
ms.openlocfilehash: d83c3d35c4cf65ebf714b44bc9db7db36b11f818
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="monitor-appliance-health-state"></a>監視應用裝置健全狀況狀態
本主題說明如何使用管理主控台，或透過直接查詢 SQL Server PDW 動態管理檢視監視 SQL Server PDW 應用裝置的狀態。  
  
## <a name="to-monitor-the-appliance-state"></a>若要監視的應用裝置狀態  
系統管理員可以使用管理主控台或 SQL Server PDW 動態管理檢視 (Dmv) 來擷取節點、 元件和軟體的完整階層架構。 下圖提供高層級的了解 SQL Server PDW 監視的元件。  
  
![監視概觀](./media/monitor-appliance-health-state/SQL_Server_PDW_Monitoring_Overview.png "SQL_Server_PDW_Monitoring_Overview")  
  
### <a name="monitor-component-status-by-using-the-admin-console"></a>使用系統管理員主控台的監視元件狀態  
若要使用管理主控台，以擷取元件狀態：  
  
1.  按一下**應用裝置狀態** 索引標籤。  
  
2.  應用裝置狀態 頁面上，按一下 檢視 節點詳細資料的特定節點上。  
  
    ![PDW 管理主控台狀態](./media/monitor-appliance-health-state/SQL_Server_PDW_AdminConsol_State.png "SQL_Server_PDW_AdminConsol_State")  
  
### <a name="monitor-component-status-by-using-system-views"></a>使用系統檢視表的監視元件狀態  
若要使用系統檢視表擷取元件狀態，請使用[sys.dm_pdw_component_health_status](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)。 例如，下列查詢會擷取所有元件的狀態。  
  
```sql  
SELECT   
   s.[pdw_node_id],  
   n.[name] as [node_name],  
   n.[address] ,  
   g.[group_id] ,  
   g.[group_name] ,  
   c.[component_id] ,  
   c.[component_name] ,  
   s.[component_instance_id] ,   
   p.[property_name] ,  
   s.[property_value] ,  
   s.[update_time]  
FROM [sys].[dm_pdw_component_health_status] AS s  
JOIN sys.dm_pdw_nodes AS n   
   ON s.[pdw_node_id] = n.[pdw_node_id]  
JOIN [sys].[pdw_health_components] AS c   
   ON s.[component_id] = c.[component_id]  
JOIN [sys].[pdw_health_component_groups] AS g   
   ON c.[group_id] = g.[group_id]  
JOIN [sys].[pdw_health_component_properties] AS p   
   ON s.[property_id] = p.[property_id] AND s.[component_id] = p.[component_id]  
WHERE p.property_name = 'Status'  
ORDER BY  
   s.[pdw_node_id],  
   g.[group_name] ,   
   s.[component_instance_id] ,  
   c.[component_name] ,   
   p.[property_name];  
```  
  
傳回的狀態屬性的可能值為：  
  
-   確定  
  
-   非關鍵性  
  
-   嚴重  
  
-   Unknown  
  
-   不支援  
  
-   無法連線  
  
-   無法復原  
  
若要查看所有元件的所有屬性，請移除`WHERE  p.property_name = 'Status'`子句。  
  
**[Update_time]**欄會顯示最後一次輪詢 SQL Server PDW 健康狀態代理程式的元件。  
  
> [!CAUTION]  
> 請務必調查此問題，當元件未被決議 5 分鐘或更久。可能表示有問題軟體的活動訊號警示。  
  
## <a name="see-also"></a>請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[應用裝置監視 &#40;Analytics Platform System &#41;](appliance-monitoring.md)  
  
