---
title: "LOWER (SSIS 運算式) | Microsoft Docs"
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
  - "將大寫字元轉換為小寫字元"
  - "LOWER 函數"
  - "大寫字元 [Integration Services]"
  - "小寫字元"
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 33
---
# LOWER (SSIS 運算式)
  傳回將大寫字元轉換為小寫字元之後的字元運算式。  
  
## 語法  
  
```  
  
LOWER(character_expression)  
```  
  
## 引數  
 *character_expression*  
 是轉換成小寫字元的字元運算式。  
  
## 結果類型  
 DT_WSTR  
  
## 備註  
 LOWER 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LOWER 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和 [Cast &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果引數為 Null，則 LOWER 會傳回 Null 結果。  
  
## 運算式範例  
 此範例會將字串常值轉換成小寫字元。 傳回結果為 "new york"。  
  
```  
LOWER("New York")  
```  
  
 此範例會將 **Color** 輸入資料行中的所有字元轉換成小寫字元，除了第一個字元以外。 如果 Color 是 YELLOW，則傳回結果為 "Yellow"。 如需詳細資訊，請參閱 [SUBSTRING &#40;SSIS Expression&#41;](../../integration-services/expressions/substring-ssis-expression.md) (SUBSTRING (SSIS 運算式))。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 此範例會將 **CityName** 變數中的值轉換成小寫字元。  
  
```  
LOWER(@CityName)  
```  
  
## 請參閱＜  
 [UPPER &#40;SSIS 運算式&#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  