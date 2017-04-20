---
title: "從舊版 SQL Server 匯入原生與字元格式資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "舊版 [SQL Server], 匯入和匯出資料格式"
  - "-V 參數"
  - "資料格式 [SQL Server], 舊版"
  - "舊版 [SQL Server], 匯入和匯出資料格式"
ms.assetid: e644696f-9017-428e-a5b3-d445d1c630b3
caps.latest.revision: 40
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 40
---
# 從舊版 SQL Server 匯入原生與字元格式資料
  在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中，您可以透過 **-V** 參數使用 **bcp**，從 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 匯入原生與字元格式資料。 **-V** 參數會讓 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 使用指定之舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料類型，而資料檔案格式將會與舊版中的資料檔案格式相同。  
  
 若要為資料檔案指定舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請使用 **-V** 參數搭配下列其中一個限定詞：  
  
|SQL Server 版本|Qualifier|  
|------------------------|---------------|  
|[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]|**-V80**|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|**-V90**|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|**-V100**|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|**-V 110**|  
  
## 資料類型的解譯  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新的版本支援一些新的類型。 如果您想要將新的資料類型匯入舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，您必須以舊版 **bcp** 用戶端可讀取的格式儲存該資料類型。 下表摘述如何轉換新資料類型，以便與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相容。  
  
|SQL Server 2005 的新資料類型|與 6*x* 版相容的資料類型|與 70 版相容的資料類型|與 80 版相容的資料類型|  
|---------------------------------------|-------------------------------------------|-----------------------------------------|-----------------------------------------|  
|**bigint**|**decimal**|**decimal**|*|  
|**sql_variant**|**text**|**nvarchar(4000)**|*|  
|**varchar(max)**|**text**|**text**|**text**|  
|**nvarchar(max)**|**ntext**|**ntext**|**ntext**|  
|**varbinary(max)**|**image**|**image**|**image**|  
|XML|**ntext**|**ntext**|**ntext**|  
|UDT**|**image**|**image**|**image**|  
  
 *這是原本就支援的類型。  
  
 **UDT 表示使用者定義類型。  
  
## 使用 –V 80 匯出  
 當您使用 **–V80** 參數大量匯出資料時，處於原生模式的 **nvarchar(max)**、**varchar(max)**、**varbinary(max)**、XML 和 UDT 資料會與 4 位元組前置詞一起儲存，就像 **text**、**image** 和 **ntext** 資料一樣，而不是與 8 位元組前置詞一起儲存 (這是 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 及更新版本的預設值)。  
  
## 複製日期值  
 **bcp** 會使用 ODBC 大量複製 API。 因此，若要將日期值匯入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，**bcp** 會使用 ODBC 日期格式 (*yyyy-mm-dd hh:mm:ss*[*.f...*])。  
  
 **bcp** 命令會針對 **datetime** 和 **smalldatetime** 值使用 ODBC 預設格式來匯出字元格式資料檔案。 例如，包含日期 `12 Aug 1998` 的 **datetime** 資料行會以字元字串 `1998-08-12 00:00:00.000` 大量複製到資料檔案。  
  
> [!IMPORTANT]  
>  使用 **bcp** 將資料匯入 **smalldatetime** 欄位時，請確定秒數值是 00.000；否則作業將會失敗。 **smalldatetime** 資料類型只會保留最接近分鐘數的數值。 BULK INSERT 及 INSERT ...SELECT * FROM OPENROWSET(BULK...) 在這個案例中將不會失敗，但會截斷秒數值。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要使用大量匯入或大量匯出的資料格式**  
  
-   [使用字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 字元格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [使用 Unicode 原生格式匯入或匯出資料 &#40;SQL Server&#41;](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## 另請參閱  
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SQL Server Database Engine 回溯相容性](../../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
  
  