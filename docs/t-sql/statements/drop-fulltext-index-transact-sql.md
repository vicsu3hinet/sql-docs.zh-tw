---
title: "DROP FULLTEXT INDEX (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_INDEX_TSQL
- DROP FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- deleting full-text indexes
- removing full-text indexes
- full-text indexes [SQL Server], removing
- DROP FULLTEXT INDEX statement
- dropping full-text indexes
ms.assetid: 7443a4ab-1d43-4a22-bbba-a07f620892cb
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 24fdad5b47230cf22dd8d19c1ea269dffa2705b9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="drop-fulltext-index-transact-sql"></a>DROP FULLTEXT INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  從指定的資料表或索引檢視中移除全文檢索索引。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP FULLTEXT INDEX ON table_name  
```  
  
## <a name="arguments"></a>引數  
 *table_name*  
 這是要移除的全文檢索索引所在的資料表或索引檢視的名稱。  
  
## <a name="remarks"></a>備註  
 在使用 DROP FULLTEXT INDEX 命令之前，您不需要從全文檢索索引中卸除所有資料行。  
  
## <a name="permissions"></a>Permissions  
 使用者必須具有 ALTER 權限的資料表或索引檢視表，或必須屬於**sysadmin**固定伺服器角色或**db_owner**或**db_ddladmin**固定資料庫角色。  
  
## <a name="examples"></a>範例  
 下列範例會卸除存在於 `JobCandidate` 資料表中的全文檢索索引。  
  
```  
USE AdventureWorks2012;  
GO  
DROP FULLTEXT INDEX ON HumanResources.JobCandidate;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [sys.fulltext_indexes &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [全文檢索搜尋](../../relational-databases/search/full-text-search.md)  
  
  
