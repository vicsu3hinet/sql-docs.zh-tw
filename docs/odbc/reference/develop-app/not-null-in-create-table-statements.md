---
title: "在 CREATE TABLE 陳述式中非 NULL |Microsoft 文件"
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf0f66a1d3a5d1c7bb07ef90d25c61a99e7a7786
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="not-null-in-create-table-statements"></a>未在 CREATE TABLE 陳述式中的 NULL
不支援某些資料庫，並特別桌面資料庫， **NOT NULL**中的資料行條件約束**CREATE TABLE**陳述式。 如需詳細資訊，請參閱中的 SQL_NON_NULLABLE_COLUMNS 選項[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函式描述。
