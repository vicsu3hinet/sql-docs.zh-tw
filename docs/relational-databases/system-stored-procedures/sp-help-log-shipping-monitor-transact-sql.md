---
title: "(TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_monitor_TSQL
- sp_help_log_shipping_monitor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_monitor
ms.assetid: a4e96c45-6dcd-471a-a494-b5c619459855
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96e9b3f2fa8e040789b15e0969fbb4de6ccb9e00
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sphelplogshippingmonitor-transact-sql"></a>sp_help_log_shipping_monitor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回包含主要、次要或監視伺服器中已註冊的主要和次要資料庫的狀態和其他資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_help_log_shipping_monitor  
```  
  
## <a name="arguments"></a>引數  
 無。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**status**|**bit**|記錄傳送資料庫的代理程式整體狀態：<br /><br /> **0** = 狀況良好並沒有代理程式失敗。<br /><br /> **1**否則 =。|  
|**is_primary**|**bit**|指出這個資料列是否為主要資料庫的資料列：<br /><br /> **1** = 該資料列與主要資料庫。<br /><br /> **0** = 該資料列與次要資料庫。|  
|**伺服器**|**sysname**|這個資料庫所在的主要或次要伺服器的名稱。|  
|**database_name**|**sysname**|資料庫名稱。|  
|**time_since_last_backup**|**int**|前次記錄備份之後的時間長度 (以分鐘為單位)。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**last_backup_file**|**nvarchar(500)**|前次順利完成的記錄備份檔的名稱。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**backup_threshold**|**int**|前次備份之後到產生 threshold_alert 錯誤之前的時間長度 (以分鐘為單位)。 **backup_threshold**是**int**，預設值是**60 分鐘**。<br /><br /> NULL = 資訊無法取得或不相干。<br /><br /> 這個值可以使用變更[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**is_backup_alert_enabled**|**bit**|指定是否可以警示引發的時機**backup_threshold**超過。 其中一個值 (**1**)，預設值，表示，將會引發警示。<br /><br /> NULL = 資訊無法取得或不相干。<br /><br /> 這個值可以使用變更[sp_add_log_shipping_primary_database &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql.md).|  
|**time_since_last_copy**|**int**|複製前一個記錄備份之後的時間長度 (以分鐘為單位)。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**last_copied_file**|**nvarchar(500)**|前次順利複製的記錄備份檔的名稱。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**time_since_last_restore**|**int**|還原前一個記錄備份之後的時間長度 (以分鐘為單位)。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**last_restored_file**|**nvarchar(500).**|前次順利還原的記錄備份檔的名稱。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**last_restored_latency**|**int**|從建立前一個備份至還原備份所經歷的持續時間 (以分鐘為單位)。<br /><br /> NULL = 資訊無法取得或不相干。|  
|**restore_threshold**|**int**|在產生警示之前，還原作業之間所能經歷的時間 (以分鐘為單位)。 **restore_threshold**不能是 NULL。|  
|**is_restore_alert_enabled**|**bit**|指定是否產生警示時**restore_threshold**超過。 其中一個值 (**1**)，預設值，表示產生警示。<br /><br /> NULL = 資訊無法取得或不相干。<br /><br /> 若要設定還原臨界值，請使用[sp_add_log_shipping_secondary_database](../../relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql.md)。|  
  
## <a name="remarks"></a>備註  
 **sp_help_log_shipping_monitor**必須從執行**主要**監視伺服器上的資料庫。  
  
## <a name="permissions"></a>Permissions  
 需要 **系統管理員 (sysadmin)** 固定伺服器角色中的成員資格。  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server &#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
