---
title: "KEY_ID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Key_ID
- Key_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], symmetric keys
- KEY_ID function
- symmetric keys [SQL Server], IDs
- IDs [SQL Server], symmetric keys
ms.assetid: d7309542-dbbe-41dc-b42e-5d9a1c8b4838
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fb01508366558f7d5f755db50efb4a5a5b0d937d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="keyid-transact-sql"></a>KEY_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回目前資料庫中對稱金鑰的識別碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
Key_ID ( 'Key_Name' )  
```  
  
## <a name="arguments"></a>引數  
 **'** *Key_Name* **'**  
 資料庫中的對稱金鑰名稱。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 暫時金鑰的名稱，必須以數字符號 (#) 開頭。  
  
## <a name="permissions"></a>Permissions  
 由於暫時金鑰只能用在建立它們的工作階段當中，因此存取它們無需任何權限。 若要存取的是非暫時金鑰，呼叫端就必須對金鑰具備某種權限，而且絕對不能拒絕過該金鑰的 VIEW 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-id-of-a-symmetric-key"></a>A. 傳回對稱金鑰的識別碼  
 下列範例會傳回 `ABerglundKey1` 這個金鑰的識別碼。  
  
```  
SELECT KEY_ID('ABerglundKey1');  
```  
  
### <a name="b-returning-the-id-of-a-temporary-symmetric-key"></a>B. 傳回暫時對稱金鑰的識別碼  
 下列範例會傳回暫時對稱金鑰的識別碼。 請注意 `#` 是附加在金鑰名稱的前面。  
  
```  
SELECT KEY_ID('#ABerglundKey2');  
```  
  
## <a name="see-also"></a>請參閱＜  
 [KEY_GUID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/key-guid-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
