---
title: "setClientInfo 方法 (java.util.Properties) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2a8ec0b-40a2-44d1-90d9-a810d4132e56
caps.latest.revision: "19"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1628c14e94290e4f6528a09994075b5405b0e2a3
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="setclientinfo-method-javautilproperties"></a>setClientInfo 方法 (java.util.Properties)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  設定連接用戶端資訊屬性的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
public void setClientInfo (java.util.Properties properties)  
```  
  
#### <a name="parameters"></a>參數  
 *屬性*  
  
 屬性包含的物件，若要設定的用戶端資訊屬性的清單。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 SetClientInfo 方法 java.sql.Connection 介面中所指定此 setClientInfo 方法。  
  
 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]不支援任何用戶端資訊屬性。 如果這個方法會產生警告*屬性*輸入的參數不是指空的屬性集。 換句話說，這個方法會針對應用程式將要設定的屬性產生警告。 應用程式應該使用[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)方法[SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)類別來擷取每個警告。  
  
## <a name="see-also"></a>請參閱＜  
 [setClientInfo 方法 &#40;SQLServerConnection &#41;](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)   
 [SQLServerConnection 成員](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [SQLServerConnection 類別](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
