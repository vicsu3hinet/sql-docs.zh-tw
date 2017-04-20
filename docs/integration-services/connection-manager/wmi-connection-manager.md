---
title: "WMI 連接管理員 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "連接 [Integration Services], WMI"
  - "連接管理員 [Integration Services], WMI"
  - "WMI 連接管理員 [Integration Services]"
ms.assetid: fbfa4ba7-3d0d-4d6b-94ad-50741a88d03d
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# WMI 連接管理員
  WMI 連接管理員可讓封裝利用 Windows Management Instrumentation (WMI)，來管理企業環境中的資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的 Web 服務工作會使用 WMI 連線管理員。  
  
 當您將 WMI 連線管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 WMI 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。 連線管理員的 **ConnectionManagerType** 屬性會設為 **WMI**。  
  
## 設定 WMI 連接管理員  
 您可以利用下列方式設定 WMI 連接管理員：  
  
-   指定伺服器的名稱。  
  
-   指定伺服器上的命名空間。  
  
-   選取驗證模式以連接到伺服器。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的相關資訊，請參閱 [WMI 連線管理員編輯器](../../integration-services/connection-manager/wmi-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的相關資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和[以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## 請參閱＜  
 [Web 服務工作](../../integration-services/control-flow/web-service-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  