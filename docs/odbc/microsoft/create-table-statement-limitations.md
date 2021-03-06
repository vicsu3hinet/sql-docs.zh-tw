---
title: "建立資料表陳述式的限制 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0d8f73082a87978bf735e2e44f97987ba34ffbb5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="create-table-statement-limitations"></a>建立資料表陳述式的限制
使用 Microsoft Access、 Microsoft Excel 或 Paradoxdriver 時，文字或二進位資料行長度未指定 （或指定為 0），資料行的長度會設定為 255。  
  
 使用 dBASE 驅動程式時，文字或二進位資料行長度未指定 （或指定為 0），資料行長度將會設定為 254。  
  
 支援最多 255 個資料行。  
  
 無法建立 MicrosoftExcel 5.0 版，7.0 或 97 資料來源時，工作表上使用 Microsoft Excel 驅動程式時，具有相同名稱做為先前卸除工作表。 存取版本 5.0、 7.0、 或 97 工作表使用 Microsoft Excel 驅動程式時，DROP TABLE 陳述式清除工作表中，但不會刪除工作表的名稱。  
  
 使用 Paradox 驅動程式時，索引的資料表上已定義後即無法加入資料行。 如果 CREATE TABLE 陳述式的引數清單的第一個資料行建立索引，第二個資料行不會包含引數清單中。
