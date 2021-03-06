---
title: "教學課程：準備伺服器進行複寫 | Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
helpviewer_keywords: replication [SQL Server], tutorials
ms.assetid: ce30a095-2975-4387-9377-94a461ac78ee
caps.latest.revision: "15"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ff54e23da202e1161c7cc34502f79481cd3a1534
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="tutorial-preparing-the-server-for-replication"></a>教學課程：準備伺服器進行複寫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 在設定複寫拓撲之前，規劃安全性是很重要的步驟。 此教學課程為您示範：如何讓複寫拓撲有更強固的保護，以及如何設定散發，這是複寫資料的第一步。 您必須完成此教學課程，才能進行任何其他教學課程。  
  
> [!NOTE]  
> 若要在伺服器之間安全地複寫資料，必須實作 [複寫安全性最佳做法](../../relational-databases/replication/security/replication-security-best-practices.md)中的所有建議。  
  
## <a name="what-you-will-learn"></a>學習內容  
在此教學課程中，您將學習如何準備伺服器，以便在最低權限下安全地執行複寫。 第 1 課示範如何建立用來執行複寫代理程式的 Windows 服務帳戶。 第 2 課示範如何設定用來產生及儲存發行集快照集的資料夾。 第 3 課示範如何設定散發及設定權限。  
  
## <a name="requirements"></a>需求  
此教學課程是特別提供給熟悉基本資料庫作業但只稍微涉獵複寫作業的使用者。  
  
若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 與 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫。  
  
**完成本教學課程的估計時間：30 分鐘。**  
  
## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
  
-   [第 1 課：建立用於複寫的 Windows 帳戶](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
-   [第 2 課：準備快照集資料夾](../../relational-databases/replication/lesson-2-preparing-the-snapshot-folder.md)  
  
-   [第 3 課：設定散發](../../relational-databases/replication/lesson-3-configuring-distribution.md)  
  
[開始教學課程](../../relational-databases/replication/lesson-1-creating-windows-accounts-for-replication.md)  
  
## <a name="see-also"></a>另請參閱  
[設定散發](../../relational-databases/replication/configure-distribution.md)  
[安全性與保護 &#40;複寫&#41;](../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  
  
