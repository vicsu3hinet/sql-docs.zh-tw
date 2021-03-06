---
title: sys.dm_io_pending_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_io_pending_io_requests
- dm_io_pending_io_requests
- dm_io_pending_io_requests_TSQL
- sys.dm_io_pending_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_pending_io_requests dynamic management view
ms.assetid: d1fb46dd-5c74-4c04-9ecf-8934b1bedb5b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9430879bbac6a9f92c4b67553d4caa756e1cd85f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmiopendingiorequests-transact-sql"></a>sys.dm_io_pending_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中每一項暫止 I/O 要求，各傳回一個資料列。  
  
> [!NOTE]  
>  若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_io_pending_io_requests**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**io_completion_request_address**|**varbinary(8)**|IO 要求的記憶體位址。 不可為 Null。|  
|**io_type**|**varchar(7)**|暫止 I/O 要求的類型。 不可為 Null。|  
|**io_pending**|**int**|指出 I/O 要求是否暫止，或已由 Windows 完成。 I/O 要求仍然暫止，即使 Windows 已完成該要求，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尚未執行內容切換，來處理 I/O 要求及從這份清單中移除它。 不可為 Null。|  
|**io_completion_routine_address**|**varbinary(8)**|完成 I/O 要求時要呼叫的內部函數。 可為 Null。|  
|**io_user_data_address**|**varbinary(8)**|僅供內部使用。 可為 Null。|  
|**scheduler_address**|**varbinary(8)**|發出這項 I/O 要求所在的排程器。 I/O 要求將出現在排程器的暫止 I/O 清單上。 如需詳細資訊，請參閱[sys.dm_os_schedulers &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md). 不可為 Null。|  
|**io_handle**|**varbinary(8)**|用於 I/O 要求之檔案的檔案控制代碼。 可為 Null。|  
|**io_offset**|**bigint**|I/O 要求的位移。 不可為 Null。|  
|**io_pending_ms_ticks**|**int**|僅供內部使用。 不可為 Null。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。  
 

  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [我 O 相關動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


