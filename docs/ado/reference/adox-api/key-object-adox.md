---
title: "索引鍵物件 (ADOX) |Microsoft 文件"
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
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9a1f971c07571c54cc74e4a750fde505e60af2f2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="key-object-adox"></a>索引鍵的物件 (ADOX)
代表資料庫資料表中的主要、 外部索引鍵，或唯一索引鍵欄位。  
  
## <a name="remarks"></a>備註  
 下列程式碼建立新**金鑰**:  
  
```  
Dim obj As New Key  
```  
  
 與屬性和集合**金鑰**物件，您可以：  
  
-   識別與金鑰[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   判斷索引鍵是否為主要，外部索引鍵，或唯一的[類型](../../../ado/reference/adox-api/type-property-key-adox.md)屬性。  
  
-   存取資料庫的資料行與索引鍵[資料行](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定與相關聯的資料表名稱[RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md)屬性。  
  
-   判斷在刪除或更新具有主索引鍵上執行的動作[DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)和[UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md)屬性。  
  
 本章節包含下列主題。  
  
-   [Key 物件屬性、方法和事件](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
