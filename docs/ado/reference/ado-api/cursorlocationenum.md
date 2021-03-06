---
title: CursorLocationEnum | Microsoft Docs
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
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52bd88c7d2f5916e33094c085296f5fec8f99d28
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
指定資料指標服務的位置。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|會使用本機資料指標程式庫所提供的用戶端資料指標。 本機資料指標服務通常會讓驅動程式提供資料指標，可能的許多功能而使用這項設定可能會提供一項優點對於將啟用的功能。 回溯相容性，同義字**adUseClientBatch**也支援。|  
|**adUseNone**|1|不使用資料指標服務。 （這個常數已經過時，僅為了回溯相容性會出現）。|  
|**adUseServer**|2|預設值。 會使用資料提供者或驅動程式所提供的資料指標。 這些資料指標是有時候非常大的彈性，並允許其他敏感度其他資料來源所做的變更。 不過，某些功能[OLE DB 的 Microsoft 資料指標服務](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md)，例如取消關聯<br /><br /> [資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)無法模擬與伺服器端資料指標的物件，以及這些功能將無法使用這項設定。|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 對等項目  
 Package: **com.ms.wfc.data**  
  
|常數|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>適用於  
 [CursorLocation 屬性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
