---
title: "getLockTimeout 方法 (SQLServerDataSource) |Microsoft 文件"
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
apiname: SQLServerDataSource.getLockTimeout
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 676094e9-ec18-4524-9b21-1f9c5b16dd52
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6134888c8c4d2ef9c499e2423e9b14acccbbf91b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="getlocktimeout-method-sqlserverdatasource"></a>getLockTimeout 方法 (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  傳回**int**值，指出資料庫要等候報告鎖定逾時之前的毫秒數。  
  
## <a name="syntax"></a>語法  
  
```  
  
public int getLockTimeout()  
```  
  
## <a name="return-value"></a>傳回值  
 **Int**值，包含資料庫要等候的毫秒數。  
  
## <a name="remarks"></a>備註  
 鎖定逾時是等候資料庫報告鎖定逾時的毫秒數。預設值為 -1，表示將會無限期地等候。 如果已指定，則此值為連接上所有陳述式的預設值。  
  
> [!NOTE]  
>  0 值表示不會等候。 如果未設定 lockTimeout 屬性，getLockTimeout 方法會傳回預設值 -1。  
  
## <a name="see-also"></a>請參閱＜  
 [SQLServerDataSource 成員](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [SQLServerDataSource 類別](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
