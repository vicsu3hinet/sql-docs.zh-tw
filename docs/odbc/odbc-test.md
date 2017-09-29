---
title: "ODBC 測試 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC test [ODBC]
- ODBC drivers [ODBC], testing
- gtrtst32.dll
- gtrts32w.dll [ODBC]
- odbct32w.exe [ODBC]
- odbcte32.exe [ODBC]
- testing ODBC drivers [ODBC]
ms.assetid: 7f13894c-5697-436c-be3d-fe16e1a02325
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c5396150d9b3ae7e3c79fa3568c1468f775cb8e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="odbc-test"></a>ODBC 測試
Microsoft® ODBC 測試是 ODBC 的應用程式可讓您測試 ODBC 驅動程式和 ODBC 驅動程式管理員。 ODBC 3.51 包含 ANSI 和 unicode 版本的 ODBC 測試。 對應檔案如下所示：  
  
-   Odbcte32.exe 和 Gtrtst32.dll，ANSI 版本。  
  
-   Odbct32w.exe 和 Gtrts32w.dll，Unicode 版本。  
  
 若要使用 ODBC 測試，您必須了解 ODBC API 的 C 語言和 SQL。 如需 ODBC API 的詳細資訊，請參閱[ODBC 程式設計人員參考](../odbc/reference/odbc-programmer-s-reference.md)。  
  
 先前包含在這個區段中的文件的說明主題現在包含在 ODBC 測試程式。 開啟 Odbcte32.exe 或 Odbct32w.exe，開啟**協助**功能表，然後再按一下**說明主題**。  
  
 請注意，這些應用程式，適用於 64 位元 Microsoft Windows 作業系統的 64 位元版本相同的名稱與 32 位元版本，即使它們是不同的檔案。 也就是 64 位元版本的 ODBC 測試的 Unicode 版本的名稱是 odbct32w.exe。