---
title: "ROLLBACK TRANSACTION (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROLLBACK TRANSACTION
- ROLLBACK
- ROLLBACK_TSQL
- ROLLBACK_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transaction rollbacks [SQL Server]
- ROLLBACK TRANSACTION statement
- erasing data modifications [SQL Server]
- rolling back transactions, ROLLBACK TRANSACTION
- roll back transactions [SQL Server]
- savepoints [SQL Server]
ms.assetid: 6882c5bc-ff74-476a-984b-164aeb036c66
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 0df2fdf3d3e4aa7915fbfef3ff921d12b2851044
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="rollback-transaction-transact-sql"></a>ROLLBACK TRANSACTION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  將明確或隱含的交易回復到交易的開頭，或回復到交易內的儲存點。 您可以使用 ROLLBACK TRANSACTION 清除交易開始之後的所有資料修改，或清除儲存點之前的所有資料修改。 另外，它也會釋出交易所保留的資源。  
  

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ROLLBACK { TRAN | TRANSACTION }   
     [ transaction_name | @tran_name_variable  
     | savepoint_name | @savepoint_variable ]   
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *transaction_name*  
 指派給 BEGIN TRANSACTION 之交易的名稱。 *transaction_name*必須符合識別碼規則，但使用的交易名稱的前 32 個字元。 當建立巢狀交易， *transaction_name*必須是從最外層的 BEGIN TRANSACTION 陳述式的名稱。 *transaction_name*一定是區分大小寫，即使執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不區分大小寫。  
  
 **@** *tran_name_variable*  
 這是包含有效交易名稱之使用者定義變數的名稱。 變數必須宣告與**char**， **varchar**， **nchar**，或**nvarchar**資料型別。  
  
 *savepoint_name*  
 是*savepoint_name*從 SAVE TRANSACTION 陳述式。 *savepoint_name*必須符合識別碼的規則。 使用*savepoint_name*條件式回復時應該會影響屬於交易。  
  
 **@** *savepoint_variable*  
 這是包含有效儲存點名稱之使用者自訂變數的名稱。 變數必須宣告與**char**， **varchar**， **nchar**，或**nvarchar**資料型別。  
  
## <a name="error-handling"></a>錯誤處理  
 ROLLBACK TRANSACTION 陳述式不會產生任何訊息給使用者。 如果在預存程序或觸發程序中需要警告，請使用 RAISERROR 或 PRINT 陳述式。 RAISERROR 是指示錯誤的慣用陳述式。  
  
## <a name="general-remarks"></a>一般備註  
 ROLLBACK TRANSACTION，而不*savepoint_name*或*transaction_name*復原回交易的開頭。 當建立巢狀交易時，這個相同的陳述式會回復所有內部交易，直到最外層的 BEGIN TRANSACTION 陳述式。 在這兩種情況下，ROLLBACK TRANSACTION 會遞減 @@TRANCOUNT系統函式設為 0。 ROLLBACK TRANSACTION *savepoint_name*不會使@TRANCOUNT。  
  
 ROLLBACK TRANSACTION 無法參考*savepoint_name*分散式交易中明確啟動 BEGIN DISTRIBUTED TRANSACTION，或從本機交易擴大。  
  
 在執行 COMMIT TRANSACTION 陳述式之後，無法回復交易，但是當 COMMIT TRANSACTION 與所要回復之交易內含的巢狀交易相關聯時，則為例外。 在本例中，巢狀的交易會會回復，即使您已為其發出 COMMIT TRANSACTION。  
  
 交易內可以有重複的儲存點名稱，但使用重複儲存點名稱的 ROLLBACK TRANSACTION 只會回復到最近一個使用這個儲存點名稱的 SAVE TRANSACTION。  
  
## <a name="interoperability"></a>互通性  
 預存程序，不含 ROLLBACK TRANSACTION 陳述式*savepoint_name*或*transaction_name*所有陳述式回復到最外層的 BEGIN TRANSACTION。 @ 會導致預存程序中的 ROLLBACK TRANSACTION 陳述式@TRANCOUNT比的預存程序完成時，有不同的值以 @@TRANCOUNT值呼叫預存程序時所產生資訊訊息。 這個訊息不會影響後續的處理。  
  
 如果在觸發程序內發出 ROLLBACK TRANSACTION：  
  
-   目前交易中到這個點為止所進行的所有資料修改都會被回復，其中包括觸發程序所進行的任何修改。  
  
-   觸發程序會在 ROLLBACK 陳述式之後，繼續執行任何其餘陳述式。 如果有任何這些陳述式修改資料，不會回復這些修改。 執行這些其餘陳述式並不會引發巢狀觸發程序。  
  
-   不會執行在引發觸發程序的陳述式之後的批次中之陳述式。  
  
@@TRANCOUNT輸入觸發程序，即使在自動認可模式下時，以一遞增。 (系統會將觸發程序當做一項隱含的巢狀交易來處理。)  
  
預存程序中的 ROLLBACK TRANSACTION 陳述式並不會影響在批次中呼叫程序的後續陳述式；仍會執行批次中的後續陳述式。 觸發程序中的 ROLLBACK TRANSACTION 陳述式會終止包含引發觸發程序之陳述式的批次；不會繼續執行批次中的後續陳述式。  
  
下列三個規則定義 ROLLBACK 對資料指標的作用：  
  
1.  當 CURSOR_CLOSE_ON_COMMIT 設為 ON，ROLLBACK 會關閉所有開啟的資料指標，但不會將它們取消配置。  
  
2.  當 CURSOR_CLOSE_ON_COMMIT 設為 OFF，ROLLBACK 不會影響任何開啟的同步 STATIC 或非感應式資料指標，或已充分擴展的非同步 STATIC 資料指標。 任何其他類型的開啟資料指標都會關閉，但不會取消配置。  
  
3.  終止批次且會產生內部回復的錯誤，會將包含錯誤陳述式之批次中所宣告的所有資料指標取消配置。 所有資料指標都會取消配置，不論它們的類型或 CURSOR_CLOSE_ON_COMMIT 設定為何，都是如此。 其中包括錯誤批次呼叫的預存程序中所宣告之資料指標。 在錯誤批次之前的批次中宣告的資料指標會遵守規則 1 和 2。 死結錯誤就是這類型錯誤的範例。 觸發程序中所發出之 ROLLBACK 陳述式也會自動產生這類錯誤。  
  
## <a name="locking-behavior"></a>鎖定行為  
 ROLLBACK TRANSACTION 陳述式指定*savepoint_name*釋放於儲存點，但是擴大和轉換除外之後所取得的鎖定。 這些鎖定不會被釋放，也不會轉換回之前的鎖定模式。  
  
## <a name="permissions"></a>Permissions  
 需要 **public** 角色中的成員資格。  
  
## <a name="examples"></a>範例  
 下列範例顯示回復具名交易的作用。 之後建立的資料表，下列陳述式啟動具名的交易、 插入兩個資料列，並會復原交易在變數中名為@TransactionName。 具名交易外的另一個陳述式會插入兩個資料列。 查詢會傳回前一個陳述式的結果。   
  
```sql    
USE tempdb;  
GO  
CREATE TABLE ValueTable ([value] int);  
GO  
  
DECLARE @TransactionName varchar(20) = 'Transaction1';  
  
BEGIN TRAN @TransactionName  
       INSERT INTO ValueTable VALUES(1), (2);  
ROLLBACK TRAN @TransactionName;  
  
INSERT INTO ValueTable VALUES(3),(4);  
  
SELECT [value] FROM ValueTable;  
  
DROP TABLE ValueTable;  
```  
[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]  
```  
value  
-----   
3    
4  
```  
  
  
## <a name="see-also"></a>另請參閱  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION (TRANSACT-SQL)](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)   
 [認可工作 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK WORK &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)  
  
  
