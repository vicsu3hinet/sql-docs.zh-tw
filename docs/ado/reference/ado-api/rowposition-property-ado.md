---
title: "RowPosition 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction::put_RowPosition
- ADORecordConstruction::PutRowPosition
- ADORecordConstruction::GetRowPosition
- ADORecordConstruction::RowPosition
- ADORecordConstruction::get_RowPosition
helpviewer_keywords:
- RowPosition property [ADO]
ms.assetid: 9d068fed-39bf-4842-afc3-686a2af2145d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e384d850a51cc94439a896040951ec3c23f2f6a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="rowposition-property-ado"></a>RowPosition 屬性 (ADO)
取得或設定 OLE DB **RowPosition**物件上從 / **ADORecordsetConstruction**物件。 當您使用**put_RowPosition**設定**RowPosition**物件，產生**資料錄集**物件會使用**RowPosition**物件判斷目前的資料列。  
  
 讀取/寫入  
  
## <a name="syntax"></a>語法  
  
```  
HRESULT get_RowPosition([out, retval] IUnknown** ppRowPos);  
HRESULT put_RowPosition([in] IUnknown* pRowPos);  
```  
  
## <a name="parameters"></a>參數  
 *ppRowPos*  
 OLE DB 指標**RowPosition**物件。  
  
 *PRowPos*  
 OLE DB **RowPosition**物件。  
  
## <a name="return-values"></a>傳回值  
 這個屬性的方法會傳回標準的 HRESULT 值，包括 S_OK 和 E_FAIL。  
  
## <a name="remarks"></a>備註  
 當這個屬性設定時，如果**資料列集**物件上**RowPosition**物件與不同**資料列集**物件上**資料錄集**物件，前者會覆寫後者。 相同的行為套用至目前**章**的**RowPosition**以及。  
  
## <a name="applies-to"></a>適用於  
 [ADORecordsetConstruction 介面](../../../ado/reference/ado-api/adorecordsetconstruction-interface.md)
