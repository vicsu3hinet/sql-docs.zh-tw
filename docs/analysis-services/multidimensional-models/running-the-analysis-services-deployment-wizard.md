---
title: "執行 Analysis Services 部署精靈 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Analysis Services 部署精靈, 執行"
ms.assetid: 3a38d489-4625-4878-bd18-c6f903be33df
caps.latest.revision: 41
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 38
---
# 執行 Analysis Services 部署精靈
  當您使用「 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈」來部署 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案時，可依下列方式執行此精靈：  
  
-   **互動式** ：以互動方式執行時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈會產生以輸入檔為基礎的 XML 部署指令碼，而由使用者輸入以互動方式加以修改。 精靈只會將使用者修改套用至部署指令碼。 精靈不會修改輸入檔。 如需關於輸入檔的詳細資訊，請參閱[了解用來建立部署指令碼的輸入檔](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md)。  
  
-   **從命令提示字元**：在命令提示字元下執行時，「[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈」會以您用來執行精靈的參數為基礎，而產生 XML for Analysis \(XMLA\) 部署指令碼。 此精靈可以是下列其中之一：提示使用者輸入並依據該輸入來修改輸入檔；依現狀使用輸入檔來執行無訊息自動部署；或建立可稍後使用的部署指令碼。  
  
## 以互動方式執行 Analysis Services 部署精靈  
 當您以互動方式執行時， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈會從輸入檔讀取值，並呈現此資訊。 您可以修改這些輸入值—例如部署目的地、組態設定、部署選項和連接字串密碼—或保留現狀。 如果您變更輸入值，在產生 XMLA 部署指令碼時，精靈會使用這些變更。 不過，精靈不會對輸入檔中的值做任何變更。  
  
> [!NOTE]  
>  如果您想要讓 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈修改輸入值，請在命令提示字元下執行精靈，並設定精靈在回應檔案模式中執行。  
  
 在檢閱輸入值和進行任何變更之前，精靈會產生 XMLA 部署指令碼。 您可以在目的地伺服器上立即執行此部署指令碼，或儲存指令碼供稍後使用。  
  
#### 以互動方式執行 Analysis Services 部署精靈  
  
-   按一下 **[開始]**功能表，依序指向 **[所有程式]**、 **[Microsoft SQL Server]**和 **[Analysis Services]**，然後按一下 **[部署精靈]**。  
  
     – 或 –  
  
-   在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案的 [專案] 資料夾中，按兩下 *\<專案名稱\>*.asdatabase 檔案。  
  
    > [!NOTE]  
    >  如果您找不到 *\<專案名稱\>*.asdatabase 檔案，請試著使用 [搜尋] 功能並指定 \*.asdatabase。  
  
## 在命令提示字元下執行 Analysis Services 部署精靈  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈也可以在命令提示字元下執行。 當您在命令提示字元中執行精靈時，請提供 .asdatabase 檔案的完整路徑，並在下列其中一個模式下執行精靈：  
  
 **回應檔案模式**  
 在回應檔案模式中，精靈可讓您以互動方式修改 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 專案在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中建立時原先產生的輸入檔。 在產生 XMLA 部署指令碼之前，精靈會儲存這些修改的輸入檔。 下次執行精靈時，已修改的輸入檔會變成新的起點。  
  
 若要在回應檔案模式中執行精靈，請使用 **\//a** 參數。  
  
 **無訊息模式**  
 在無訊息模式中，精靈會依據輸入檔的資訊來執行無訊息自動部署。  
  
 若要在無訊息模式中執行精靈，請使用 **\//s** 參數。 當您在無訊息模式中執行精靈時，訊息會輸出到主控台，或是所提供的記錄檔。  
  
 **輸出模式**  
 在輸出模式中，精靈會依據輸入檔產生 XMLA 部署指令碼供稍後執行。  
  
 若要在輸出模式中執行精靈，請使用 **\//o** 參數並提供輸出檔名稱。  
  
 如需關於這些命令列參數的詳細資訊，請參閱[使用部署公用程式的部署模型方案](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)。  
  
 下列程序描述如何在命令提示字元下執行 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 部署精靈。  
  
#### 在命令提示字元下執行 Analysis Services 部署精靈  
  
1.  開啟命令提示字元，並瀏覽至 C:\\Program Files \(x86\)\\Microsoft SQL Server\\120\\Tools\\Binn\\ManagementStudio  
  
2.  輸入 **Microsoft.AnalysisServices.Deployment.exe** ，後面接著您要用於執行精靈之模式的對應參數。  
  
## 另請參閱  
 [了解 Analysis Services 部署指令碼](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)   
 [Deploy Model Solutions Using the Deployment Wizard](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  