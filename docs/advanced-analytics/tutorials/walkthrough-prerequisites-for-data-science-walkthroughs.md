---
title: "SQL Server R 的資料科學逐步解說的必要條件 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0b0582b8-8843-4787-94a8-2e28bdc04fb2
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b9d3a579f023a7e6d9805b934edc3f0e9e5ad5e8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="prerequisites-for-the-data-science-walkthrough-for-sql-server-and-r"></a>SQL Server R 的資料科學逐步解說的必要條件

我們建議您本逐步解說膝上型電腦或其他電腦上已安裝的 Microsoft R 程式庫。 您必須能夠連接，在相同的網路，到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]機器學習服務與啟用的 R 語言的電腦。

您可以同時具有在電腦上執行此逐步解說[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和 R 開發環境，但我們不建議此組態，在實際執行環境。

## <a name="install-machine-learning-for-sql-server"></a>安裝 SQL Server 的機器學習服務

您必須能夠存取 SQL Server 的執行個體，可以支援 R 安裝，請使用下列其中一項：

+ 機器學習服務 （資料庫） for SQL Server 2017
+ SQL Server 2016 R Services

如需詳細資訊，請參閱[設定 SQL Server R 服務 (資料庫內](../r/set-up-sql-server-r-services-in-database.md)。

> [!IMPORTANT]
> 請務必使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或更新版本。 舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支援 R 整合。不過，您可以使用 SQL 資料庫做為 ODBC 資料來源。

## <a name="install-an-r-development-environment"></a>安裝 R 開發環境

這個逐步解說中，我們建議您使用 R 開發環境。 以下是一些建議：

- **Visual Studio 的 R 工具**(RTVS) 是一套免費提供 Intellisense、 偵錯，並支援 Microsoft。 您可以使用它與 R Server 和 SQL Server 機器學習服務的外掛程式。 若要下載，請參閱 [適用於 Visual Studio 的 R 工具](https://www.visualstudio.com/features/rtvs-vs.aspx)。

- **Microsoft R Client** 是輕量級開發工具，可支援在 R 中使用 ScaleR 封裝進行開發。 若要取得它，請參閱 [開始使用 Microsoft R Client](https://msdn.microsoft.com/microsoft-r/r-client-get-started)。

- **RStudio** 是其中一個比較常見的 R 開發環境。 如需詳細資訊，請參閱 [https://www.rstudio.com/products/RStudio/](https://www.rstudio.com/products/RStudio/)。

    您無法完成本教學課程中使用的一般安裝 RStudio 或其他環境。您也必須安裝 R 封裝和連線程式庫的 Microsoft R Open。 如需詳細資訊，請參閱 [Set Up a Data Science Client](../r/set-up-a-data-science-client.md)(設定資料科學用戶端)。

- 當您安裝基本的 R 工具 (R.exe，RTerm.exe，RScripts.exe) 也會依預設安裝[!INCLUDE[rsql_rro-noversion](../../includes/rsql-rro-noversion-md.md)]。 如果您不想要安裝的 IDE，您可以使用這些工具。

## <a name="get-permissions-on-the-sql-server-instance-and-database"></a>取得 SQL Server 執行個體和資料庫上的權限

若要連接到的執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行指令碼和上傳資料，您必須具有有效的登入資料庫伺服器上。  您可以使用 SQL 登入或整合式 Windows 驗證。 詢問資料庫管理員，您可以使用： 在資料庫中設定下列權限的帳戶

- 建立資料庫、資料表、函數和預存程序
- 寫入資料至資料表
- 執行 R 指令碼的能力 (`GRANT EXECUTE ANY EXTERNAL SCRIPT to <user>`)

這個逐步解說中，我們也可以使用 SQL 登入**RTestUser**。 通常建議使用 Windows 整合式的驗證，但使用的 SQL 登入會簡單一些示範進行。

## <a name="change-list"></a>變更清單

+ 此範例的原始開發使用 SQL Server 2016 R Services。 不過，重大變更是導入的 Microsoft R 元件在 2016 SP1。 具體來說， _varsToDrop_和_varsToKeep_不再支援 SQL Server 資料來源的參數。 Therefre，如果您已經下載版的教學課程在 SP1 之前，它將無法再使用 post SP1 組建。

+ 使用 SQL Server 2017 機器學習服務 （RC1 和 RC2） 的發行前組建的測試目前版本的範例。 一般情況下，幾乎所有的步驟應該 2016 SP1 和 2017年之間執行而不需修改。

## <a name="next-lesson"></a>下一課

[準備要使用 PowerShell 的資料](/walkthrough-prepare-the-data.md)
