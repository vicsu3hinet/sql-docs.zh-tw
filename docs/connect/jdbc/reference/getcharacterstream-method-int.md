---
title: "getCharacterStream 方法 (int) |Microsoft 文件"
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
apiname: SQLServerResultSet.getCharacterStream (int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f345dc0fe0c52b4c70d280fbbd6c893095dbf36c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getcharacterstream-method-int"></a>getCharacterStream 方法 (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  擷取值，這個目前的資料列內指定之資料行索引的[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)物件當做 java.io.Reader 物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>參數  
 *columnIndex*  
  
 **Int** ，指出資料行索引。  
  
## <a name="return-value"></a>傳回值  
 讀取器物件。  
  
## <a name="exceptions"></a>例外狀況  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>備註  
 GetCharacterStream 方法 java.sql.ResultSet 介面中所指定這個 getCharacterStream 方法。  
  
 這個方法只會讀取[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Unicode 字元資料類型，例如 nchar、 nvarchar、 nvarchar （max） 和 ntext。 所有其他資料型別 (包括 ASCII 字元型別) 將擲回例外狀況。 若要讀取 ASCII 資料型別，使用[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)方法。  
  
## <a name="see-also"></a>請參閱＜  
 [getCharacterStream 方法 &#40;SQLServerResultSet &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 成員](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 類別](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
