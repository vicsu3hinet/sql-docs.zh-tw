---
title: "unwrap 方法 (SQLServerXADataSource) |Microsoft 文件"
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
ms.assetid: d97c99b3-2224-4abb-8b32-40aff49fe759
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a59d9a1a7bf80f96bc509a6793703de9caa884d6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="unwrap-method-sqlserverxadatasource"></a>unwrap 方法 (SQLServerXADataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回物件，用於實作指定的介面，以允許存取[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-特有的方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>參數  
 *iface*  
  
 類型的類別之**T**定義介面。  
  
## <a name="return-value"></a>傳回值  
 物件，可實作指定的介面。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 [Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverxadatasource.md)方法由 JDBC 4.0 規格中導入的 java.sql.Wrapper 介面所定義。  
  
 應用程式可能需要存取特有的 JDBC api 延伸模組[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]。 Unwrap 方法支援解除包裝成為這個物件可延伸，公用類別，在類別公開供應商延伸模組。  
  
 [SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)類別會擴充[SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)類別，後者從擴充[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)類別。 呼叫這個方法時，物件會解除包裝成為下列類別： [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerXADataSource](../../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
 如需詳細資訊，請參閱[包裝函式和介面](../../../connect/jdbc/wrappers-and-interfaces.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerXADataSource 方法](../../../connect/jdbc/reference/sqlserverxadatasource-methods.md)   
 [SQLServerXADataSource 成員](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [SQLServerXADataSource 類別](../../../connect/jdbc/reference/sqlserverxadatasource-class.md)  
  
  
