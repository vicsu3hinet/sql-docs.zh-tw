---
title: "STNumCurves (geography 資料類型) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|spatial-geography
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STNumCurves
- STNumCurves_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STNumCurves method (geography)
ms.assetid: e98a56c2-8496-4dfd-9b37-7f3c4ca9b2b5
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b7baccab2b0087fdb2ae90f5b212b4d820919d25
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="stnumcurves-geography-data-type"></a>STNumCurves (geography 資料類型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  傳回一維的曲線數目**geography**執行個體。  
  
## <a name="syntax"></a>語法  
  
```  
  
.STNumCurves()  
```  
  
## <a name="return-types"></a>傳回類型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回型別：**地理位置**  
  
 CLR 傳回類型： **SqlGeography**  
  
## <a name="remarks"></a>備註  
 一維空間資料類型包括**LineString**， **CircularString**，和**CompoundCurve**。 空的一維**geography**執行個體會傳回 0。  
  
 `STNumCurves`（） 只適用於簡單類型。不適用於**geography**集合喜歡**MultiLineString**。 **NULL**時，會傳回**geography**執行個體不是一維資料類型。  
  
 **Null**會傳回未初始化**geography**執行個體。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-stnumcurves-on-a-circularstring-instance"></a>A. 在 CircularString 執行個體上使用 STNumCurves()  
 下列範例會顯示如何取得 `CircularString` 執行個體中的曲線數目：  
  
```
 DECLARE @g geography; 
 SET @g = geography::Parse('CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)');  
 SELECT @g.STNumCurves();
 ```  
  
### <a name="b-using-stnumcurves-on-a-compoundcurve-instance"></a>B. 在 CompoundCurve 執行個體上使用 STNumCurves()  
 下列範例會使用 `STNumCurves()` 傳回 `CompoundCurve` 執行個體中的曲線數目。  
  
```
 DECLARE @g geography;  
 SET @g = geography::Parse('COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))');  
 SELECT @g.STNumCurves();
 ```  
  
## <a name="see-also"></a>另請參閱  
 [空間資料類型概觀](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [地理例項上的 OGC 方法](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
