---
title: "將自訂位置加入至地圖 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "MICROSOFT.REPORTDESIGNER.MAPPOINT.POINTTEMPLATE"
ms.assetid: 7d36faae-5bcc-446a-9eba-f42349cafacb
caps.latest.revision: 10
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# 將自訂位置加入至地圖 (報表產生器及 SSRS)
  將地圖加入至 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表後，您可以加入自己的點位置。  
  
 圖層上所有點的顯示屬性都可以透過設定圖層之點屬性的選項來控制。 若是選取的內嵌點，您可以覆寫顯示屬性。  
  
> [!NOTE]  
>  當您覆寫內嵌點的圖層顯示屬性時，無法回復您所做的變更。  
  
 如需詳細資訊，請參閱[使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 加入點圖層  
  
1.  在報表設計介面上，按一下地圖來選取它，然後顯示 [地圖] 窗格。  
  
2.  在工具列上，按一下 [加入圖層]。  
  
3.  從下拉式清單中，按一下 [加入點圖層]。 不含點的點圖層便會加入至地圖中。 根據預設，內嵌點的點圖層已經準備就緒。  
  
## 加入自訂點  
  
1.  在報表設計介面上，按一下地圖來選取它，然後顯示 [地圖] 窗格。  
  
2.  在 [地圖] 窗格中，以滑鼠右鍵按一下 [內嵌] 類型的點圖層，然後按一下 [加入點]。 游標會變更為十字形狀。  
  
3.  若要加入點，按一下地圖上的某個位置。 內嵌點就會加入至您所按之位置的選定圖層。  
  
## 若要自訂內嵌點的顯示  
  
1.  以滑鼠右鍵按一下點，然後按一下 [點屬性]。 [地圖內嵌點屬性] 對話方塊隨即開啟。  
  
2.  按一下 [覆寫此圖層的點選項]。 多個屬性頁面隨即出現在左窗格。  
  
3.  按一下這些頁面，然後設定您要套用到這個點的顯示屬性。  
  
## 請參閱＜  
 [地圖 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [使用規則與分析資料更改多邊形、線條與點顯示 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/vary polygon, line, and point display by rules and analytical data.md)  
  
  