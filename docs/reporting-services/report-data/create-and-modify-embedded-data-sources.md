---
title: "建立和修改內嵌資料來源 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
  - "reporting-services-sharepoint"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c38c2e8-7a29-4f79-a4a3-85ed2b13723b
caps.latest.revision: 10
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 10
---
# 建立和修改內嵌資料來源
  內嵌資料來源是定義在報表定義中，而且只能供該報表使用。  
  
## 在報表設計師中建立內嵌資料來源  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]** ，然後按一下 **[資料來源]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
    > [!NOTE]  
    >  如果看不到 [報表資料] 窗格，請按一下 [檢視] 功能表上的 [報表資料]。  
  
2.  在 **[名稱]** 文字方塊中，輸入資料來源的名稱或接受預設值。 資料來源名稱是在報表內部使用。 為了清楚起見，我們建議資料來源的名稱要包含連接字串中所指定的資料庫名稱。  
  
3.  確認 [內嵌連接]  已選取，然後執行下列動作。  
  
    1.  從 [類型] 下拉式清單中，選取資料來源類型，例如 [Microsoft SQL Server] 或 [OLE DB]。  
  
    2.  使用以下其中一個替代方式指定連接字串：  
  
        -   在 **[連接字串]** 文字方塊中直接輸入連接字串。 如需連接字串範例的清單，請參閱[報表產生器中的資料連接、資料來源及連接字串](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md)或[資料連接、資料來源及連接字串 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)。  
  
        -   按一下運算式 (**fx)** 按鈕，即可建立一個評估為連接字串的運算式。 在 **[運算式]** 對話方塊的 [運算式] 窗格內，輸入運算式。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   按一下 **[編輯]** ，針對您在步驟 2 中選擇的資料來源類型開啟 **[連接屬性]** 對話方塊。  
  
             依照此資料來源類型適合的情況，填入 **[連接屬性]** 對話方塊中的欄位。 連接屬性包括資料來源的類型、資料來源的名稱以及要使用的認證。 當您在此對話方塊中指定值之後，請按一下 **[測試連接]** 來確認此資料來源確實可用，而且您指定的認證正確無誤。 如需特定資料來源類型的詳細資訊，請參閱[從外部資料來源加入資料 &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md)。  
  
    3.  按一下 **[認證]**。  
  
         指定用於這個資料來源的認證。 資料來源的擁有者會選擇支援的認證類型。  
  
4.  新的內嵌資料來源會出現在 [報表資料] 窗格中。  
  
## 在報表產生器中建立內嵌資料來源  
  
1.  在 [報表資料] 窗格的工具列上，按一下 **[新增]**，然後按一下 **[資料來源]**。 **[資料來源屬性]** 對話方塊隨即開啟。  
  
2.  在 **[名稱]** 文字方塊中，輸入資料來源的名稱或接受預設值。  
  
3.  確認已選取 **[使用內嵌於我的報表的連接]** 。  
  
    1.  從 [選取連接類型] 下拉式清單中，選取資料來源類型，例如 [Microsoft SQL Server] 或 [OLE DB]。  
  
    2.  使用以下其中一個替代方式來指定連接字串：  
  
        -   在 **[連接字串]** 文字方塊中直接輸入連接字串。 如需連接字串範例的清單，請參閱[報表產生器中的資料連接、資料來源及連接字串](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md)。  
  
        -   按一下運算式 (**fx)** 按鈕，即可建立一個評估為連接字串的運算式。 在 **[運算式]** 對話方塊的 [運算式] 窗格內，輸入運算式。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
        -   按一下 **[建立]** ，針對您在步驟 2 中選擇的資料來源類型開啟 **[連接屬性]** 對話方塊。  
  
             依照此資料來源類型適合的情況，填入 **[連接屬性]** 對話方塊中的欄位。 連接屬性包括資料來源的類型、資料來源的名稱以及要使用的認證。 當您在此對話方塊中指定值之後，請按一下 **[測試連接]** 來確認此資料來源確實可用，而且您指定的認證正確無誤。  
  
4.  按一下 **[認證]**。  
  
     指定用於這個資料來源的認證。 資料來源的擁有者會選擇支援的認證類型。 如需詳細資訊，請參閱[在報表產生器中指定認證](../Topic/Specify%20Credentials%20in%20Report%20Builder.md)。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     資料來源會出現在 [報表資料] 窗格中。  
  
## 請參閱＜  
 [報表內嵌資料集和共用資料集 &#40;報表產生器和 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [在報表產生器中指定認證](../Topic/Specify%20Credentials%20in%20Report%20Builder.md)  
  
  