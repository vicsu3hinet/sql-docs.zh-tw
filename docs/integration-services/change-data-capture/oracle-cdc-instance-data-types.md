---
title: "Oracle CDC 執行個體資料類型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eec13d8d-c15a-4542-bfc4-da66b1a6bfe0
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Oracle CDC 執行個體資料類型
  Oracle CDC 執行個體支援大多數的 Oracle 資料類型。 以下章節描述支援的資料類型和不支援的資料類型。  
  
## 支援的資料類型  
 下表描述可以擷取的 Oracle 資料類型，以及變更資料表中這些類型與 SQL Server 資料類型的預設對應。 為來源 Oracle 資料表加入擷取執行個體時，您可以覆寫這些對應的一部分。  
  
|Oracle 資料庫資料類型|SQL Server 資料類型|  
|-------------------------------|--------------------------|  
|BINARY_FLOAT|REAL|  
|BINARY_DOUBLE|FLOAT|  
|CHAR|NVARCHAR|  
|DATE|DATETIME|  
|FLOAT|FLOAT|  
|INT|NUMERIC (38)|  
|INTERVAL|DATETIME|  
|NCHAR|NVARCHAR|  
|NUMBER|FLOAT|  
|NAVARCHAR2|NVARCHAR|  
|RAW|VARBINARY|  
|REAL|FLOAT|  
|TIMESTAMP|DATETIME2|  
|TIMESTAMP WITH TIME ZONE|VARCHAR (37)|  
|TIMESTAMP WITH LOCAL TIME ZONE|VARCHAR (37)|  
|VARCHAR2|VARCHAR|  
|XMLTYPE|NVARCHAR (MAX)|  
  
## 不支援的資料類型  
 如果來源 Oracle 資料表中的資料行具有以下 Oracle 資料類型，則無法擷取這些資料表。 如果擷取的資料行具有這些資料類型，則會顯示為 null；但是，其值的變更會在擷取之資料表的變更遮罩中指示。  
  
-   LONG  
  
-   XMLTYPE  
  
-   BLOB  
  
-   CLOB  
  
 如果來源 Oracle 資料表中的資料行具有以下 Oracle 資料類型，則無法擷取這些資料表。  
  
-   BFILE  
  
-   ROWID  
  
-   REF  
  
-   UROWID  
  
-   巢狀資料表  
  
 如果資料表中有以下資料類型存在，這些資料類型會讓 LogMinder 無法針對資料表的任何資料行取得任何資料：  
  
-   使用者定義資料類型  
  
-   VARRAY  
  
## 請參閱＜  
 [Attunity Oracle 異動資料擷取設計工具](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Oracle CDC 執行個體](../../integration-services/change-data-capture/the-oracle-cdc-instance.md)  
  
  