---
title: "資料錄集相關的錯誤資訊 |Microsoft 文件"
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
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b1ad53c42fa3da686de10e3254c6fa7e3916d806
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="recordset-related-error-information"></a>資料錄集相關的錯誤資訊
批次在處理期間，**狀態**屬性**資料錄集**物件提供資訊中的個別記錄**資料錄集**。 批次更新所需的位置，先**狀態**屬性**資料錄集**反映要加入、 變更和刪除記錄的相關資訊。 之後**UpdateBatch**呼叫之後**狀態**屬性會指出成功或失敗的作業。 當您移動記錄記錄**資料錄集**，值**狀態**屬性變更來描述目前記錄的狀態。
