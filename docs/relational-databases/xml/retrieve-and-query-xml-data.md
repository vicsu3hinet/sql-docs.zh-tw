---
title: "擷取及查詢 XML 資料 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "XML 資料 [SQL Server], 擷取"
  - "XML 執行個體擷取"
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# 擷取及查詢 XML 資料
  本主題說明查詢 XML 資料必須指定的查詢選項。 也會描述當 XML 執行個體儲存於資料庫中時，未保留的 XML 執行個體部分。  
  
##  <a name="features"></a> 未保留的 XML 執行個體功能  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會保留 XML 執行個體的內容，但是不會保留在 XML 資料模型中不視為重大之 XML 執行個體的層面。 這表示擷取的 XML 執行個體可能不等於儲存於伺服器上的執行個體，但是將會包含相同的資訊。  
  
### XML 宣告  
 若執行個體儲存於資料庫中，就不會保留執行個體中的 XML 宣告。 例如：  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 結果為 `<doc/>`。  
  
 將 XML 資料儲存於 `<?xml version='1.0'?>`資料類型執行個體內時，不會保留 XML 宣告 (例如 **xml** )。 這是原廠設定。 XML 宣告 () 及其屬性 (version/encoding/stand-alone) 在將資料轉換成 **xml** 類型之後會遺失。 XML 宣告會被視為 XML 剖析器的指示詞。 XML 資料會當做 ucs-2 儲存於內部。 XML 執行個體中的所有其他 PI 都會保留下來。  
  
 [本主題內容](#top)  
  
### 屬性順序  
 XML 執行個體中屬性的順序不會被保留。 當您查詢 **xml** 類型資料行中儲存的 XML 執行個體時，產生之 XML 中的屬性順序可能會與原始 XML 執行個體不一樣。  
  
 [本主題內容](#top)  
  
### 屬性值兩側的引號  
 屬性值兩側的單引號與雙引號不會保留。 屬性值會當做成對的名稱/值儲存在資料庫中。 引號則不會儲存。 當您針對 XML 執行個體執行 XQuery 時，產生的 XML 會序列化並以雙引號括住屬性值。  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 兩個查詢都會傳回 = `<root a="1" />`。  
  
 [本主題內容](#top)  
  
### 命名空間前置詞  
 命名空間前置詞不會保留。 當您針對 **xml** 類型的資料行指定 XQuery 時，序列化的 XML 結果可能會傳回不同的命名空間前置詞。  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 結果中的命名空間前置詞可能會不同。 例如：  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
 [本主題內容](#top)  
  
##  <a name="query"></a> 設定必要查詢選項  
 使用 **xml** 資料類型方法來查詢 **xml** 類型資料行或變數時，必須依下表所示，設定下列選項。  
  
|SET 選項|必要值|  
|-----------------|---------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNINGS|ON|  
|ARITHABORT|ON|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
  
 如果未將這些選項設為如上表所示，對於 **xml** 資料類型方法的查詢及修改都會失敗。  
  
 [本主題內容](#top)  
  
## 另請參閱  
 [建立 XML 資料的執行個體](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  