---
title: "呼叫 SQLGetDiagField |Microsoft 文件"
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
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d9a8ffdb5166840e53a7a3b05785f32d4dc1c1a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="calling-sqlgetdiagfield"></a>呼叫 SQLGetDiagField
當 ODBC 3。*x*應用程式會呼叫**SQLGetDiagField** ODBC 2*.x*驅動程式，此驅動程式會傳回 SQL_SUCCESS 中的適當資訊 *\*DiagInfoPtr*如果*Sqlgetdiagfield*引數是 SQL_DIAG_CLASS_ORIGIN SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_號碼、 SQL_DIAG_RETURNCODE SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE。 所有其他診斷欄位將會傳回 SQL_ERROR。
