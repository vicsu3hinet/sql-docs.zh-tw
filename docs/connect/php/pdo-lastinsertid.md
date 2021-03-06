---
title: "PDO::lastInsertId |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0c617b53-a74b-4d5b-b76b-3ec7f1b8e8de
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00a3f4499c4fa0dee832fb8838d8a1239ed7ff49
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="pdolastinsertid"></a>PDO::lastInsertId
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

傳回最近在資料庫的資料表中插入之資料列的識別碼。 資料表必須有 IDENTITY NOT NULL 資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
string PDO::lastInsertId ([ $name ] );  
```  
  
#### <a name="parameters"></a>參數  
$*name*：一個選擇性字串，可讓您指定資料表。  
  
## <a name="return-value"></a>傳回值  
最近加入之資料列的識別碼字串。 若方法呼叫失敗，則為空字串。  
  
## <a name="remarks"></a>備註  
[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]2.0 版已加入 PDO 支援。  
  
## <a name="example"></a>範例  
  
```  
<?php  
   $database = "test";  
   $server = "(local)";  
   $conn = new PDO( "sqlsrv:server=$server; Database = $database", "", "");  
  
   $conn->exec("use Test");  
  
   $ret = $conn->exec("INSERT INTO Table1 VALUES( '19' )");  
   $ret = $conn->exec("INSERT INTO ScrollTest VALUES( 1, '19' )");  
  
   $lastRow = $conn->lastInsertId('Table1');  
   echo $lastRow . "\n";  
  
   // defaults to ScrollTest  
   $lastRow = $conn->lastInsertId();  
   echo $lastRow . "\n";  
?>  
```  
  
## <a name="see-also"></a>另請參閱  
[PDO 類別](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
