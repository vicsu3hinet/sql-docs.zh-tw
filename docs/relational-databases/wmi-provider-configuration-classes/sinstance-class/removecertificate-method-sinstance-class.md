---
title: "RemoveCertificate 方法 （SInstance 類別） |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: RemoveCertificate Method (SInstance Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b86c693562f4aa79669252dcd3c33fef90e184bb
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="removecertificate-method-sinstance-class"></a>RemoveCertificate 方法 (SInstance 類別)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]從執行個體中移除目前的安全性憑證[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.RemoveCertificate()  
```  
  
## <a name="parts"></a>組件  
 *物件*  
 代表 [執行個體上之伺服器設定的](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md) SInstance 類別 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]物件。  
  
## <a name="property-valuereturn-value"></a>屬性值/傳回值  
 uint32 值，如果已成功修改此服務為 0，如果不支援要求則為 1，以及其他指示錯誤的任何數字。  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>請參閱＜  
 [設定伺服器網路通訊協定和網路程式庫](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  