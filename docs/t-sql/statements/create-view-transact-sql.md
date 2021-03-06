---
title: "建立檢視 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 633179d7540ba4a6515c3614724a4849f40de391
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="create-view-transact-sql"></a>CREATE VIEW (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  建立由查詢定義其內容 (資料行和資料列) 的虛擬資料表。 您可以使用這個陳述式來建立資料庫中一個或多個資料表內資料的檢視。 例如，檢視可用於下列目的：  
  
-   對焦 (Focus)、簡化和自訂每位使用者查看資料庫的角度。  
  
-   做為安全機制，讓使用者能夠透過檢視存取資料，但不將直接存取基底資料表的權限授與使用者。  
  
-   提供回溯相容介面以模擬其結構描述已變更的資料表。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] VIEW [ schema_name . ] view_name [ (column [ ,...n ] ) ]   
[ WITH <view_attribute> [ ,...n ] ]   
AS select_statement   
[ WITH CHECK OPTION ]   
[ ; ]  
  
<view_attribute> ::=   
{  
    [ ENCRYPTION ]  
    [ SCHEMABINDING ]  
    [ VIEW_METADATA ]       
}   
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE VIEW [ schema_name . ] view_name [  ( column_name [ ,...n ] ) ]   
AS <select_statement>   
[;]  
  
<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>  
```  
  
## <a name="arguments"></a>引數
或 ALTER  
 **適用於**:[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (開頭為[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1)。   
  
 只有當它已經存在，有條件地更改檢視。 
 
 *schema_name*  
 這是檢視所屬的結構描述名稱。  
  
 *view_name*  
 這是檢視的名稱。 檢視名稱必須遵照識別碼的規則。 指定檢視擁有者名稱則是選擇性的。  
  
 *資料行*  
 這是檢視中的資料行所用的名稱。 只有在資料行是從算術運算式、函數或常數衍生而來時，兩個或更多資料行可能有相同名稱 (通常是因為聯結) 時，或檢視中之資料行的指定名稱不同於衍生來源的資料行名稱時，才需要資料行名稱。 您也可以在 SELECT 陳述式中指派資料行名稱。  
  
 如果*資料行*未指定，檢視資料行取得的 SELECT 陳述式中的資料行相同的名稱。  
  
> [!NOTE]  
>  在檢視的資料行中，資料行名稱的權限適用於整個 CREATE VIEW 或 ALTER VIEW 陳述式，不論基礎資料來源為何都是如此。 例如，如果授與權限是**SalesOrderID** CREATE VIEW 陳述式中的資料行，ALTER VIEW 陳述式可以命名**SalesOrderID**資料行具有不同的資料行名稱，例如**OrderRef**，且仍有與檢視使用相關聯的權限**SalesOrderID**。  
  
 AS  
 指定檢視要執行的動作。  
  
 *select_statement*  
 這是定義檢視的 SELECT 陳述式。 陳述式可以使用多份資料表和其他檢視。 從建立的檢視之 SELECT 子句所參考的物件中進行選取，需要適當的權限。  
  
 檢視不必是一份特定資料表的資料列和資料行的簡單子集。 您可以利用任何複雜度的 SELECT 子句來建立使用多份資料表或其他檢視的檢視。  
  
 在索引檢視定義中，SELECT 陳述式必須是單一資料表陳述式，或選擇性彙總所聯結 (JOIN) 的多份資料表。  
  
 檢視定義中的 SELECT 子句不能包括下列項目：  
  
-   ORDER BY 子句，除非 SELECT 陳述式的選取清單中也有 TOP 子句  
  
    > [!IMPORTANT]  
    >  ORDER BY 子句只能用來判定 TOP 或 OFFSET 子句在檢視定義中傳回的資料列。 除非同時在查詢本身指定 ORDER BY 子句，否則 ORDER BY 子句並不保證查詢檢視時會傳回排序的結果。  
  
-   INTO 關鍵字  
  
-   OPTION 子句  
  
-   指向暫存資料表或資料表變數的參考。  
  
 因為*select_statement*使用 SELECT 陳述式，它是有效使用\<join_hint > 和\<table_hint > FROM 子句中所指定的提示。 如需詳細資訊，請參閱[FROM &#40;TRANSACT-SQL &#41;](../../t-sql/queries/from-transact-sql.md)和[SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-transact-sql.md). 
  
 函式和 UNION 或 UNION ALL 所分隔的多個 SELECT 陳述式可用於*select_statement*。  
  
 CHECK OPTION  
 強制對檢視進行中的條件集所執行的所有資料修改陳述式*select_statement*。 當利用檢視來修改資料列時，WITH CHECK OPTION 可確保在認可修改之後，仍可以透過檢視見到資料。  
  
> [!NOTE]  
>  直接更新檢視的基礎資料表，不會針對檢視來進行驗證，即使指定了 CHECK OPTION 也是如此。  
  
 ENCRYPTION  
 **適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 中的項目會加密[sys.syscomments](../../relational-databases/system-compatibility-views/sys-syscomments-transact-sql.md)中包含 CREATE VIEW 陳述式文字。 使用 WITH ENCRYPTION 可防止在 SQL Server 複寫中發行檢視。  
  
 SCHEMABINDING  
 將檢視繫結於一或多份基礎資料表的結構描述。 當指定 SCHEMABINDING 時，無法依照會影響檢視定義的方式來修改一或多份基底資料表。 您必須先修改或卸除檢視定義來移除對於要修改之資料表的相依性。 當您使用 SCHEMABINDING 時， *select_statement*必須包含兩部分名稱 (*結構描述***。***物件*) 的資料表、 檢視或所參考的使用者定義函數。 所有參考的物件都必須在相同的資料庫中。  
  
 您無法卸除參與 SCHEMABINDING 子句所建立之檢視的檢視或資料表，除非這份檢視已經卸除或有了改變，不再擁有結構描述繫結。 否則，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會引發錯誤。 另外，當 ALTER TABLE 陳述式會影響到檢視定義時，在參與擁有結構描述繫結的檢視之資料表上執行這些陳述式也會失敗。  
  
 VIEW_METADATA  
 指定當針對參考檢視的查詢來要求瀏覽模式的中繼資料時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體將檢視 (而不是一份或多份基底資料表) 的中繼資料資訊傳回 DB-Library、ODBC 和 OLE DB API。 瀏覽模式中繼資料是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體傳回給用戶端 API 的附加中繼資料。 這個中繼資料使得用戶端 API 能夠實作可更新的用戶端資料指標。 瀏覽模式中繼資料包括結果集中的資料行所屬之基底資料表的相關資訊。  
  
 如果是 VIEW_METADATA 所建立的檢視，當描述結果集中檢視的資料行時，瀏覽模式中繼資料會傳回檢視名稱，而不是基底資料表名稱。  
  
 當檢視利用 WITH VIEW_METADATA，其所有資料行，建立除非**時間戳記**資料行，您可以更新，如果檢視有 INSTEAD OF INSERT 或 INSTEAD OF UPDATE 觸發程序。 如需有關可更新檢視的詳細資訊，請參閱「備註」一節。  
  
## <a name="remarks"></a>備註  
 檢視只能建立在目前資料庫中。 CREATE VIEW 必須是查詢批次中的第一個陳述式。 檢視最多可有 1,024 個資料行。  
  
 當查詢檢視時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會檢查確定陳述式所參考的所有資料庫物件都存在、在陳述式的內容中有效，且修改資料陳述式未違反任何資料完整性規則。 檢查失敗會傳回錯誤訊息。 檢查成功會將動作轉換成針對基礎資料表的動作。  
  
 如果檢視相依於已卸除的資料表或檢視，任何人試圖使用這份檢視時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 一律會產生錯誤訊息。 如果建立新的資料表或檢視，且並未變更先前基底資料表的資料表結構來取代已卸除的資料表或檢視，此時又可以使用這份檢視。 如果新資料表或檢視的結構有了改變，就必須卸除再重新建立這份檢視。  
  
 如果檢視未以 SCHEMABINDING 子句建立[sp_refreshview](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)變更會影響檢視定義的物件基礎的檢視時應執行。 否則，在查詢檢視時，可能會產生非預期的結果。  
  
 建立檢視時，要將檢視的相關資訊儲存在下列目錄檢視： [sys.views](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)， [sys.columns](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)，和[sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)。 CREATE VIEW 陳述式的文字會儲存在[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)目錄檢視。  
  
 使用索引檢視的查詢定義與**數值**或**float**運算式可能不會使用索引檢視的類似查詢與不同的結果。 這個差異可能是基礎資料表的 INSERT、DELETE 或 UPDATE 動作期間之捨入錯誤所造成的。  
  
 當建立檢視時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會儲存 SET QUOTED_IDENTIFIER 和 SET ANSI_NULLS 的設定。 當使用這份檢視時，會利用這些原始設定來剖析檢視。 因此，當存取檢視時，SET QUOTED_IDENTIFIER 和 SET ANSI_NULLS 的任何用戶端工作階段設定都不會影響這個檢視定義。  
  
## <a name="updatable-views"></a>可更新的檢視  
 只要符合下列條件，您可以利用檢視來修改基礎基底資料表的資料：  
  
-   包括 UPDATE、INSERT 和 DELETE 陳述式在內的任何修改都只能參考一份基底資料表的資料行。  
  
-   檢視所修改的資料行必須直接參考資料表資料行中的基礎資料。 您無法利用任何其他方法來衍生這些資料行，例如：  
  
    -   彙總函式：AVG、COUNT、SUM、MIN、MAX、GROUPING、STDEV、STDEVP、VAR 和 VARP。  
  
    -   計算。 您不能從使用其他資料行的運算式計算資料行。 利用設定運算子 UNION、UNION ALL、CROSSJOIN、EXCEPT 和 INTERSECT 形成的資料行會得出一項計算，這些資料行無法更新。  
  
-   GROUP BY、HAVING 或 DISTINCT 子句不會影響所修改的資料行。  
  
-   TOP 不用於任何地方*select_statement*搭配 WITH CHECK OPTION 子句的檢視。  
  
 先前的限制適用於檢視之 FROM 子句中的任何子查詢，正如同它們適用於檢視本身一樣。 一般而言，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 必須能夠明確地追蹤從檢視定義到一份基底資料表的修改。 如需詳細資訊，請參閱[修改資料透過檢視](../../relational-databases/views/modify-data-through-a-view.md)。  
  
 如果先前的限制使您無法直接利用檢視來修改資料，請考量下列選項：  
  
-   **而不是觸發程序**  
  
     您可以建立檢視的 INSTEAD OF 觸發程序，使檢視成為可以更新。 INSTEAD OF 觸發程序的執行是用來取代定義觸發程序的資料修改陳述式。 這個觸發程序可讓使用者指定一組為了處理資料修改陳述式而必須發生的動作。 因此，如果 INSTEAD OF 觸發程序是針對某份特定資料修改陳述式 (INSERT、UPDATE 或 DELETE) 的檢視而存在，您也可以利用這個陳述式來更新對應的檢視。 而不是觸發程序的相關資訊，請參閱[DML 觸發程序](../../relational-databases/triggers/dml-triggers.md)。  
  
-   **資料分割的檢視**  
  
     如果檢視是一份分割區檢視，在特定限制之下，這份檢視可以更新。 當需要它時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將本機分割區檢視當做所有參與的資料表及檢視本身是在相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的檢視，並將分散式分割區檢視當做檢視中至少有一份資料表是在不同伺服器或遠端伺服器的檢視。  
  
## <a name="partitioned-views"></a>分割區檢視  
 分割區檢視是成員資料表的 UNION ALL 所定義的檢視，這些成員資料表的結構相同，但在相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中，或在一群獨立存在的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器 (稱為同盟資料庫伺服器) 執行個體中，它們分別儲存成多份資料表。  
  
> [!NOTE]  
>  在伺服器本機分割資料的慣用方法是透過分割區資料表。 如需詳細資訊，請參閱 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)。  
  
 在設計分割區結構描述時，您必須清楚哪些資料屬於哪個分割區。 例如，`Customers` 資料表的資料散發在三個伺服器位置的三份成員資料表中：`Customers_33` 的 `Server1`、`Customers_66` 的 `Server2`，以及 `Customers_99` 的 `Server3`。  
  
 `Server1` 的分割區檢視定義如下：  
  
```  
--Partitioned view as defined on Server1  
CREATE VIEW Customers  
AS  
--Select from local member table.  
SELECT *  
FROM CompanyData.dbo.Customers_33  
UNION ALL  
--Select from member table on Server2.  
SELECT *  
FROM Server2.CompanyData.dbo.Customers_66  
UNION ALL  
--Select from mmeber table on Server3.  
SELECT *  
FROM Server3.CompanyData.dbo.Customers_99;  
```  
  
 一般而言，如果檢視的形式如下，它便是一份分割區檢視：  
  
```  
SELECT <select_list1>  
FROM T1  
UNION ALL  
SELECT <select_list2>  
FROM T2  
UNION ALL  
...  
SELECT <select_listn>  
FROM Tn;  
```  
  
## <a name="conditions-for-creating-partitioned-views"></a>建立分割區檢視的條件  
  
1.  選取 `list`  
  
    -   在檢視定義的資料行清單中，應該已選取成員資料表中的所有資料行。  
  
    -   每份 `select list` 的相同序數位置中之各個資料行都應該是相同類型，定序也包括在內。 資料行只是如同 UNION 的情況一樣，能夠隱含地轉換類型，是不足的。  
  
         另外，至少必須有一個資料行 (如 `<col>`) 出現在所有選取清單的相同序數位置中。 這個 `<col>` 的定義方式應該是 `T1, ..., Tn` 等成員資料表在 `C1, ..., Cn` 上分別定義了 `<col>` 等 CHECK 條件約束。  
  
         `C1` 資料表所定義之 `T1` 條件約束的形式必須如下：  
  
        ```  
        C1 ::= < simple_interval > [ OR < simple_interval > OR ...]  
        < simple_interval > :: =   
        < col > { < | > | \<= | >= | = < value >}   
        | < col > BETWEEN < value1 > AND < value2 >  
        | < col > IN ( value_list )  
        | < col > { > | >= } < value1 > AND  
        < col > { < | <= } < value2 >  
        ```  
  
    -   條件約束的方式是 `<col>` 的任何指定值都能夠滿足 `C1, ..., Cn` 等條件約束中的最多一項條件約束，因此，這些條件約束應該形成一組無關聯或不重疊的間隔。 定義無關聯的條件約束之 `<col>` 資料行稱為分割區資料行。 請注意，在基礎資料表中，分割區資料行可能會有不同的名稱。 條件約束應該在已啟用和受信任的狀態中，才能符合先前所提到的分割區資料行的條件。 如果已停用條件約束，重新啟用條件約束使用的檢查條件約束檢查*constraint_name*選項的 ALTER TABLE，並使用 WITH CHECK 選項來進行驗證。  
  
         下列範例會顯示各組有效的條件約束：  
  
        ```  
        { [col < 10], [col between 11 and 20] , [col > 20] }  
        { [col between 11 and 20], [col between 21 and 30], [col between 31 and 100] }  
        ```  
  
    -   在選取清單中，不能重複使用相同的資料行。  
  
2.  資料分割資料行  
  
    -   分割區資料行是資料表 PRIMARY KEY 的一部分。  
  
    -   無法計算、 識別、 預設或**時間戳記**資料行。  
  
    -   如果成員資料表的相同資料行有多個條件約束，Database Engine 會忽略所有條件約束，當判斷檢視是否為分割區檢視時，並不會考量它們。 若要符合分割區檢視的條件，分割區資料行只應該有一項分割區條件約束。  
  
    -   對於分割區資料行能不能更新並沒有任何限制。  
  
3.  成員資料表，或基礎資料表 `T1, ..., Tn`  
  
    -   這些資料表可以是本機資料表或正在執行以四部分名稱或基於 OPENDATASOURCE 或 OPENROWSET 的名稱來參考的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之其他電腦的資料表。 OPENDATASOURCE 和 OPENROWSET 語法可以指定資料表名稱，但不能是傳遞查詢。 如需詳細資訊，請參閱[OPENDATASOURCE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/opendatasource-transact-sql.md)和[OPENROWSET &#40;TRANSACT-SQL &#41;](../../t-sql/functions/openrowset-transact-sql.md).  
  
         如果一或多份成員資料表在遠端，這份檢視便稱為「分散式分割區檢視」，且適用其他條件。 本章節稍後會加以說明。  
  
    -   在 UNION ALL 陳述式所組合的一組資料表中，相同資料表不能出現兩次。  
  
    -   成員資料表不能有資料表的計算資料行所建立的索引。  
  
    -   成員資料表應該在相同數目的資料行上，具備所有 PRIMARY KEY 條件約束。  
  
    -   檢視中的所有成員資料表都應該有相同的 ANSI 填補設定。 這可以設定使用**使用者選項**選項**sp_configure**或 SET 陳述式。  
  
## <a name="conditions-for-modifying-data-in-partitioned-views"></a>修改分割區檢視中修改資料的條件  
 下列限制適用於在分割區檢視中修改資料的陳述式：  
  
-   INSERT 陳述式必須提供檢視中所有資料行的值，即使基礎成員資料表有這些資料行的 DEFAULT 條件約束或允許 Null 值，也是如此。 對於有 DEFAULT 定義的成員資料表資料行而言，這些陳述式不能明確使用 DEFAULT 關鍵字。  
  
-   插入分割區資料行的值應該滿足至少一個基礎條件約束；否則，插入動作會因條件約束違規而失敗。  
  
-   UPDATE 陳述式不能指定 DEFAULT 關鍵字作為 SET 子句中的值，即使資料行有對應成員資料表所定義的 DEFAULT 值也是如此。  
  
-   檢視中的多個資料行如果是一或多個成員資料表中的一個識別欄位，則無法利用 INSERT 或 UPDATE 陳述式來修改。  
  
-   如果其中一個成員資料表包含**時間戳記**資料行，無法修改資料，使用 INSERT 或 UPDATE 陳述式。  
  
-   如果成員資料表之一包含觸發程序或 ON UPDATE CASCADE/SET NULL/SET DEFAULT 或 ON DELETE CASCADE/SET NULL/SET DEFAULT 條件約束，便無法修改檢視。  
  
-   如果陳述式中有與相同檢視或任何成員資料表的自我聯結，便不允許有針對分割區檢視的 INSERT、UPDATE 和 DELETE 動作。  
  
-   不支援大量匯入資料到資料分割檢視**bcp**或 BULK INSERT 和 INSERT...SELECT * FROM OPENROWSET(BULK...) 陳述式。 不過，使用到資料分割檢視插入多個資料列[插入](../../t-sql/statements/insert-transact-sql.md)陳述式。  
  
    > [!NOTE]  
    >  若要更新分割區檢視，使用者必須有成員資料表的 INSERT、UPDATE 和 DELETE 權限。  
  
## <a name="additional-conditions-for-distributed-partitioned-views"></a>分散式分割區檢視的其他條件  
 分散式分割區檢視 (當一或多份成員資料表是在遠端) 適用下列其他條件：  
  
-   將啟動分散式交易來確保跨越更新所影響的所有節點之不可部分完成的特性。  
  
-   XACT_ABORT SET 選項應該設為 ON，INSERT、UPDATE 或 DELETE 陳述式才能夠運作。  
  
-   遠端資料表中的類型的任何資料行**smallmoney**資料分割檢視所參考之對應為**money**。 因此，本機資料表中 （在選取清單中的相同序數位置） 的對應資料行也必須是型別**money**。  
  
-   資料庫相容性層級 110 及更高，遠端資料表中的類型的任何資料行**smalldatetime**資料分割檢視所參考之對應為**smalldatetime**。 對應的資料行 （在選取清單中的相同序數位置） 本機資料表中必須是**smalldatetime**。 這是從舊版的行為變更[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]遠端資料表中的類型的任何資料行中**smalldatetime**資料分割檢視所參考之對應為**datetime**和本機資料表中的對應資料行必須是型別**datetime**。 如需詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
-   分割區檢視中的任何連結伺服器都不能是回送連結伺服器。 這是指向相同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的連結伺服器。  
  
 包含可更新的分割區檢視和遠端資料表的 INSERT、UPDATE 和 DELETE 動作，其 SET ROWCOUNT 選項的設定都會被忽略。  
  
 當成員資料表和分割區檢視定義都備妥時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢最佳化工具會建立智慧型計畫，有效地利用查詢來存取成員資料表中的資料。 當使用 CHECK 條件約束定義時，查詢處理器會跨越各份成員資料表來對應索引鍵值的散發。 當使用者發出查詢時，查詢處理器會比較這項對應與 WHERE 子句所指定的值，且會建立在成員伺服器之間傳送最少量資料的執行計畫。 因此，雖然部分成員資料表在遠端伺服器中，但 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體仍能解析分散式查詢，只需傳送最少量的散發資料。  
  
## <a name="considerations-for-replication"></a>複寫的考量  
 若要在複寫所涉及的成員資料表上建立分割區檢視，適用下列考量：  
  
-   如果基礎資料表有合併式複寫或具有更新訂閱的異動複寫中牽涉到**uniqueidentifier**也應該在選取清單中包含資料行。  
  
     資料分割檢視的任何插入動作必須提供 newid （） 值給**uniqueidentifier**資料行。 UPDATE 動作**uniqueidentifier**資料行必須提供 newid （） 值，因為無法使用 DEFAULT 關鍵字。  
  
-   利用檢視來進行的更新複寫與在兩個不同的資料庫中複寫資料表相同；這些資料表由不同複寫代理程式來提供，無法保證更新的順序。  
  
## <a name="permissions"></a>Permissions  
 至少必須有資料庫中的 CREATE VIEW 權限，以及正在建立之檢視表所在之結構描述的 ALTER 權限。  
  
## <a name="examples"></a>範例  

下列範例會使用 AdventureWorks 2012 或 AdventureWorksDW 資料庫。  

### <a name="a-using-a-simple-create-view"></a>A. 使用簡單的 CREATE VIEW  
 下列範例會利用簡單的 `SELECT` 陳述式來建立檢視。 當資料行組合的查詢頻率很高時，簡單檢視非常有用。 這份檢視的資料來自 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫的 `HumanResources.Employee` 和 `Person.Person` 資料表。 這項資料提供 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 的員工名稱和雇用日期資訊。 您可以為主管追蹤工作週年記錄的人建立這份檢視，但不提供他存取這些資料表所有資料的權利。  
  
```  
CREATE VIEW hiredate_view  
AS   
SELECT p.FirstName, p.LastName, e.BusinessEntityID, e.HireDate  
FROM HumanResources.Employee e   
JOIN Person.Person AS p ON e.BusinessEntityID = p.BusinessEntityID ;  
GO  
  
```  
  
### <a name="b-using-with-encryption"></a>B. 使用 WITH ENCRYPTION  
 下列範例會使用 `WITH ENCRYPTION` 選項，且會顯示計算資料行、重新命名的資料行和多個資料行。  
  
**適用於**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]和[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
```  
CREATE VIEW Purchasing.PurchaseOrderReject  
WITH ENCRYPTION  
AS  
SELECT PurchaseOrderID, ReceivedQty, RejectedQty,   
    RejectedQty / ReceivedQty AS RejectRatio, DueDate  
FROM Purchasing.PurchaseOrderDetail  
WHERE RejectedQty / ReceivedQty > 0  
AND DueDate > CONVERT(DATETIME,'20010630',101) ;  
GO  
  
```  
  
### <a name="c-using-with-check-option"></a>C. 使用 WITH CHECK OPTION  
 下列範例會顯示一份名稱為 `SeattleOnly` 的檢視，這份檢視參考五份資料表，可讓資料修改只套用在居住在 Seattle 的員工。  
  
```  
CREATE VIEW dbo.SeattleOnly  
AS  
SELECT p.LastName, p.FirstName, e.JobTitle, a.City, sp.StateProvinceCode  
FROM HumanResources.Employee e  
INNER JOIN Person.Person p  
ON p.BusinessEntityID = e.BusinessEntityID  
    INNER JOIN Person.BusinessEntityAddress bea   
    ON bea.BusinessEntityID = e.BusinessEntityID   
    INNER JOIN Person.Address a   
    ON a.AddressID = bea.AddressID  
    INNER JOIN Person.StateProvince sp   
    ON sp.StateProvinceID = a.StateProvinceID  
WHERE a.City = 'Seattle'  
WITH CHECK OPTION ;  
GO  
```  
  
### <a name="d-using-built-in-functions-within-a-view"></a>D. 在檢視內使用內建函數  
 下列範例會顯示包括內建函數的檢視定義。 當您使用函數時，您必須指定衍生資料行的資料行名稱。  
  
```  
CREATE VIEW Sales.SalesPersonPerform  
AS  
SELECT TOP (100) SalesPersonID, SUM(TotalDue) AS TotalSales  
FROM Sales.SalesOrderHeader  
WHERE OrderDate > CONVERT(DATETIME,'20001231',101)  
GROUP BY SalesPersonID;  
GO  

```  
  
### <a name="e-using-partitioned-data"></a>E. 使用分割區的資料  
 下列範例會使用名稱為 `SUPPLY1`、`SUPPLY2`、`SUPPLY3` 和 `SUPPLY4` 的資料表。 這些資料表對應於四個辦公室的供應者資料表，這些辦公室在不同國家 (地區)。  
  
```  
--Create the tables and insert the values.  
CREATE TABLE dbo.SUPPLY1 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 1 and 150),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY2 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 151 and 300),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY3 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 301 and 450),  
supplier CHAR(50)  
);  
CREATE TABLE dbo.SUPPLY4 (  
supplyID INT PRIMARY KEY CHECK (supplyID BETWEEN 451 and 600),  
supplier CHAR(50)  
);  
GO  
INSERT dbo.SUPPLY1 VALUES ('1', 'CaliforniaCorp'), ('5', 'BraziliaLtd')  
, ('231', 'FarEast'), ('280', 'NZ')  
, ('321', 'EuroGroup'), ('442', 'UKArchip')  
, ('475', 'India'), ('521', 'Afrique');  
GO  
--Create the view that combines all supplier tables.  
CREATE VIEW dbo.all_supplier_view  
WITH SCHEMABINDING  
AS  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY1  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY2  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY3  
UNION ALL  
SELECT supplyID, supplier  
  FROM dbo.SUPPLY4;  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="f-creating-a-simple-view"></a>F. 建立簡單的檢視  
 下列範例會藉由選取只是某些資料行從來源資料表建立檢視。  
  
```  
CREATE VIEW DimEmployeeBirthDates AS  
SELECT FirstName, LastName, BirthDate   
FROM DimEmployee;  
```  
  
### <a name="g-create-a-view-by-joining-two-tables"></a>G. 透過聯結兩個資料表建立檢視  
 下列範例會建立一個檢視使用`SELECT`陳述式搭配`OUTER JOIN`。 聯結查詢的結果填入的檢視。  
  
```  
CREATE VIEW view1  
AS 
SELECT fis.CustomerKey, fis.ProductKey, fis.OrderDateKey, 
  fis.SalesTerritoryKey, dst.SalesTerritoryRegion  
FROM FactInternetSales AS fis   
LEFT OUTER JOIN DimSalesTerritory AS dst   
ON (fis.SalesTerritoryKey=dst.SalesTerritoryKey);  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [卸除檢視 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-view-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [建立預存程序](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md)   
 [sp_refreshview &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-refreshview-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [sys.views &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

