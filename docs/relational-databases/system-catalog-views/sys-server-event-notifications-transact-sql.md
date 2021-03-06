---
title: "sys.server_event_notifications (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_event_notifications
- sys.server_event_notifications
- sys.server_event_notifications_TSQL
- server_event_notifications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_notifications catalog view
ms.assetid: 1a83a044-3130-4551-95ca-162525846ff5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1bd455fe1fed954f3e6b4d81b8b5bd47121b6c97
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysservereventnotifications-transact-sql"></a>sys.server_event_notifications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對每個伺服器層級的事件通知物件，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|伺服器事件通知名稱。 這個名稱是跨越所有伺服器層級事件通知而為唯一的。|  
|**object_id**|**int**|物件識別碼。 內是唯一的**主要**資料庫。|  
|**parent_class**|**tinyint**|父系的類別。 它一律是 100 = 伺服器。|  
|**parent_class_desc**|**nvarchar （60)**|父類別的描述。 它一律是 SERVER。|  
|**sys.internal_tables**|**int**|它一律是 0。|  
|**create_date**|**datetime**|建立日期。|  
|**modify_date**|**datetime**|上次利用 ALTER 陳述式來修改物件的日期。|  
|**服務名稱**|**nvarchar(256)**|通知所送往之目標服務的名稱。|  
|**broker_instance**|**nvarchar （128)**|具名目標服務定義所在的 Service Broker。|  
|**creator_sid**|**varbinary(85)**|執行陳述式來建立事件通知之登入的 SID。 如果事件通知定義中沒有指定 WITH FAN_IN，則為 NULL。|  
|**principal_id**|**int**|擁有這個項目的伺服器主體識別碼。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
