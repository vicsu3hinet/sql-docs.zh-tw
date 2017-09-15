---
title: "差異 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DIFFERENCE
- DIFFERENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DIFFERENCE function
- comparing SOUNDEX values
- SOUNDEX values
ms.assetid: c58ca25d-d6ea-48fa-93bb-c9374b0b2a2b
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ea034f7217d031c21cf22f6b5aaff9bf16355a9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="difference-transact-sql"></a>DIFFERENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回一個整數值來指示兩個字元運算式之 SOUNDEX 值之間的差異。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Syntax for SQL Server, Azure SQL Database, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DIFFERENCE ( character_expression , character_expression )  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 必須是英數字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)字元資料。 *character_expression*可以是常數、 變數或資料行。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 傳回的整數是相同 SOUNDEX 值中的字元數。 傳回值的範圍是 0 到 4：0 表示相似度弱或沒有相似度，4 表示相似性強或值相同。  
  
 DIFFERENCE 和 SOUNDEX 會區分定序。  
  
## <a name="examples"></a>範例  
 在下列範例的第一部份中，比較兩個非常相似的字串之 `SOUNDEX` 值。 Latin1_General 定序`DIFFERENCE`傳回值的`4`。 在下列範例中，第二部份`SOUNDEX`值用於比較兩個非常不同的字串時，和 Latin1_General 定序`DIFFERENCE`傳回值的`0`。  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 在下列範例的第一部份中，比較兩個非常相似的字串之 `SOUNDEX` 值。 Latin1_General 定序`DIFFERENCE`傳回值的`4`。 在下列範例中，第二部份`SOUNDEX`值用於比較兩個非常不同的字串時，和 Latin1_General 定序`DIFFERENCE`傳回值的`0`。  
  
```  
-- Returns a DIFFERENCE value of 4, the least possible difference.  
SELECT SOUNDEX('Green'), SOUNDEX('Greene'), DIFFERENCE('Green','Greene');  
GO  
-- Returns a DIFFERENCE value of 0, the highest possible difference.  
SELECT SOUNDEX('Blotchet-Halls'), SOUNDEX('Greene'), DIFFERENCE('Blotchet-Halls', 'Greene');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----- ----- -----------   
G650  G650  4             
  
(1 row(s) affected)  
  
----- ----- -----------   
B432  G650  0             
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱  
 [SOUNDEX &#40;TRANSACT-SQL &#41;](../../t-sql/functions/soundex-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)  
  
  

