---
title: "sys.extended_properties (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.extended_properties
- sys.extended_properties_TSQL
- extended_properties
- extended_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.extended_properties catalog view
ms.assetid: 439b7299-dce3-4d26-b1c7-61be5e0df82a
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 931d52eb19e9dcd27cc8a256650e401928805679
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="extended-properties-catalog-views---sysextendedproperties"></a>擴充屬性目錄檢視-sys.extended_properties
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  針對目前資料庫中每個擴充屬性，各傳回一個資料列。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|class|**tinyint**|可識別內容所在的項目類別。 可以是下列其中一項：<br /><br /> 0 = 資料庫<br /><br /> 1 = 物件或資料行<br /><br /> 2 = 參數<br /><br /> 3 = 結構描述<br /><br /> 4 = 資料庫主體<br /><br /> 5 = 組件<br /><br /> 6 = 類型<br /><br /> 7 = 索引<br /><br /> 10 = XML 結構描述集合<br /><br /> 15 = 訊息類型<br /><br /> 16 = 服務合約<br /><br /> 17 = 服務<br /><br /> 18 = 遠端服務繫結<br /><br /> 19 = 路由<br /><br /> 20 = 資料空間 (檔案群組或資料分割配置)<br /><br /> 21 = 資料分割函數<br /><br /> 22 = 資料庫檔案<br /><br /> 27 = 計畫指南|  
|class_desc|**nvarchar （60)**|擴充屬性所在的類別的描述。 可以是下列其中一項：<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> 參數<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> INDEX<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> DATASPACE<br /><br /> PARTITION_FUNCTION<br /><br /> DATABASE_FILE<br /><br /> PLAN_GUIDE|  
|major_id|**int**|擴充屬性所在的項目識別碼，它是根據其類別加以解譯的。 對大部分的項目來說，這是套用至類別代表的識別碼。 下面是非標準主要識別碼的解譯：<br /><br /> 如果 class 是 0，則 major_id 一律為 0。<br /><br /> 如果 class 是 1、2 或 7，則 major_id 就是 object_id。|  
|minor_id|**int**|擴充屬性所在項目的次要識別碼，它是根據其類別加以解譯的。 對於大部分的項目來說，這個值為 0；如果不是，則識別碼如下：<br /><br /> 如果 class = 1， minor_id 就是 column_id (資料行)，否則就是 0 (物件)。<br /><br /> 如果 class = 2，minor_id 就是 parameter_id。<br /><br /> 如果 class = 7，minor_id 就是 index_id。|  
|name|**sysname**|內容名稱，另外加上的 class、major_id 和 minor_id，使它成為唯一名稱。|  
|value|**sql_variant**|擴充屬性的值。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [擴充屬性目錄檢視 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)   
 [sys.fn_listextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/sys-fn-listextendedproperty-transact-sql.md)   
 [sp_addextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)   
 [sp_dropextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproperty-transact-sql.md)   
 [sp_updateextendedproperty &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-updateextendedproperty-transact-sql.md)  
  
  
