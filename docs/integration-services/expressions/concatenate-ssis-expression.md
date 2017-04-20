---
title: "+ (串連) (SSIS 運算式) | Microsoft Docs"
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
  - "串連 [Integration Services]"
  - "+ (串連運算子)"
  - "串連運算子 (+)"
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
caps.latest.revision: 37
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 37
---
# + (串連) (SSIS 運算式)
  將兩個運算式串連成一個運算式。  
  
## 語法  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## 引數  
 *expression1、expression2*  
 是任何有效的 DT_STR、DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE 資料類型運算式。  
  
## 結果類型  
 DT_WSTR  
  
## 備註  
 運算式可使用 DT_STR 和 DT_WSTR 資料類型的其中之一或兩者。  
  
 串連 DT_STR 和 DT_WSTR 資料類型會傳回 DT_WSTR 類型的結果。 字串長度是以字元表示的原始字串之長度總和。  
  
 您只能串連具有字串資料類型 DT_STR 和 DT_WSTR 的資料，或是具有「二進位大型物件區塊」(BLOB) 資料類型 DT_TEXT、DT_NTEXT 和 DT_IMAGE 的資料。 在串連發生前，其他資料類型必須明確轉換成這些資料類型的其中之一。 如需在資料類型間合法轉換的詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 兩個運算式的資料類型必須相同，或者其中一個運算式必須隱含轉換成另一個運算式的資料類型。 例如，如果串連 "Order date is " 字串和 **OrderDate** 資料行，則 **OrderDate** 中的值會隱含轉換成字串資料類型。 若要串連兩個數值，這兩個數值都必須明確轉換成字串資料類型。  
  
 串連只能使用一種 BLOB 資料類型：DT_TEXT、DT_NTEXT 或 DT_IMAGE。  
  
 如果任一元素為 Null，則結果為 Null。  
  
 字串常值必須以引號括住。  
  
## 運算式範例  
 此範例會串連 **FirstName** 和 **LastName** 資料行中的值，並在兩者之間插入空格。  
  
```  
FirstName + ' ' + LastName  
```  
  
 此範例會串連 **ZIPCode** 和 **ZIPCode+4** 變數。 兩個變數都具有字串資料類型。 **ZIPCode+4** 必須加上方括弧，這是因為變數名稱包含 + 字元。  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## 請參閱＜  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  