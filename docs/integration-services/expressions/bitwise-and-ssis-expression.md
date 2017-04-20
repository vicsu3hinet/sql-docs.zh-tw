---
title: "&amp; (位元 AND) (SSIS 運算式) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "AND，位元 AND"
  - "& (位元 AND)"
  - "位元 AND (&)"
ms.assetid: 06d2958e-66a5-44d8-8bc4-56209ebe1ff2
caps.latest.revision: 40
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 40
---
# &amp; (位元 AND) (SSIS 運算式)
  執行兩個整數值的位元 AND 運算。 它會比較其第一個運算元的每個位元和其第二個運算元的對應位元。 如果這兩個位元都是 1，則對應的結果位元會設為 1。 否則，對應的結果位元會設為 0。  
  
 兩種條件必須都是帶正負號的整數類型，或者兩種條件必須都是不帶正負號的整數類型。  
  
## 語法  
  
```  
  
integer_expression1 & integer_expression2  
  
```  
  
## 引數  
 *integer_expression1, integer_expression2*  
 已簽署或未簽署整數資料類型的任何有效運算式。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## 結果類型  
 由兩個引數的資料類型決定。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## 備註  
 如果任一個條件為 Null，則運算式結果為 Null。  
  
## 運算式範例  
 此範例會執行 **NumberA** 和 **NumberB**資料行之間的位元 AND 運算。 **NumberA** 資料行包含 3 (0000011)，且 **NumberB** 資料行包含 7 (00000111)。  
  
```  
NumberA & NumberB  
```  
  
 運算式評估結果為 3 (00000011)。  
  
 00000011  
  
 00000111  
  
 ----------\-  
  
 00000011  
  
 此範例會執行 **ReorderPoint** 和 **SafetyStockLevel** 資料行之間的位元 AND 運算。  
  
```  
ReorderPoint & SafetyStockLevel  
```  
  
 如果 **ReorderPoint** 為 10，且 **SafetyStockLevel** 為 8，則運算式評估結果為 8 (00001000)。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001000  
  
 此範例執行兩個整數之間的位元 AND 運算。  
  
```  
3 & 5   
```  
  
 運算式評估結果為 1 (00000001)。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000001  
  
## 請參閱＜  
 [&& &#40;邏輯 AND&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)   
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  