---
title: "PUBLISHINGSERVERNAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 256cdbcb82e257b1157c329a5e20e605d53d6f14
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="replication-functions---publishingservername"></a>複寫函式-PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對參與資料庫鏡像工作階段的已發行資料庫，傳回其原始發行者名稱。 這個函數是在發行集資料庫上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 簽發者執行個體端執行。 請使用它來判斷已發行資料庫的原始簽發者。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>傳回類型  
 **nvarchar**  
  
## <a name="remarks"></a>備註  
 PUBLISHINGSERVERNAME 用於所有類型的複寫中。  
  
 當資料庫鏡像工作階段存在於簽發者和鏡像夥伴執行個體之間的發行集資料庫上時，使用 PUBLISHINGSERVERNAME。  
  
 這個函數必須在發行集資料庫的內容中執行。 當 PUBLISHINGSERVERNAME 執行於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的鏡像伺服器執行個體上的發行集資料庫時，會傳回引發已發行資料庫所在的發行集執行個體名稱。 當這個函數執行於鏡像伺服器執行個體上的未發行資料庫，或是在容錯移轉之後從鏡像伺服器執行個體發行的資料庫，會傳回該鏡像伺服器執行個體的名稱。 當這個函數執行於原始簽發者執行個體時，會傳回簽發者的名稱。  
  
## <a name="see-also"></a>請參閱＜  
 [資料庫鏡像和複寫 &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [複寫函數 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  
