---
title: "教學課程：利用行動用戶端複寫資料 | Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
ms.assetid: af673514-30c7-403a-9d18-d01e1a095115
caps.latest.revision: "24"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 445e2016c22123ecce9e12ded3688fddec63ba38
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="tutorial-replicating-data-with-mobile-clients"></a>教學課程：利用行動用戶端複寫資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 對於在中央伺服器與只是偶爾連線的行動用戶端之間移動資料的問題，複寫是一個很好的解決方案。 您可以使用複寫的精靈，輕鬆設定及管理複寫拓撲。 本教學課程告訴您，如何為行動用戶端設定複寫拓撲。  
  
## <a name="what-you-will-learn"></a>學習內容  
在本教學課程中，您將使用合併複寫，從中央資料庫發行資料給一個或多個行動用戶端使用者，讓每一個使用者都取得獨一無二篩選的資料子集。 第 1 課告訴您如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立發行集。 接下來的課程會告訴您，如何建立及同步處理訂閱。  
  
## <a name="requirements"></a>需求  
此教學課程是特別提供給熟悉基本資料庫作業但對複寫經驗有限的使用者。 開始進行本教學課程之前，必須先完成 [教學課程：準備伺服器進行複寫](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md)。  
  
若要使用這個教學課程，系統上必須已安裝下列元件：  
  
-   在發行者伺服器 (來源)：  
  
    -   任何版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，除了 Express ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) 或 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 這兩種版本無法做為複寫發行者。  
  
    -   [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫。 為了加強安全性，依預設，不會安裝範例資料庫。  
  
-   訂閱者伺服器 (目的地)：  
  
    -   任何版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，除了 [!INCLUDE[ssEW](../../includes/ssew-md.md)]以外。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 不受本教學課程建立的發行集支援。  
  
    > [!NOTE]  
    > 依預設，複寫未安裝在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]中。  
  
> [!NOTE]  
> 在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，您必須使用 sysadmin 固定伺服器角色成員的登入，連接到發行者和訂閱者。  
  
**完成本教學課程的估計時間：30 分鐘。**  
  
## <a name="lessons-in-this-tutorial"></a>本教學課程中的課程  
  
-   [第 1 課：使用合併式複寫發行資料](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
-   [第 2 課：建立合併式發行集的訂閱](../../relational-databases/replication/lesson-2-creating-a-subscription-to-the-merge-publication.md)  
  
[開始教學課程](../../relational-databases/replication/lesson-1-publishing-data-using-merge-replication.md)  
  
## <a name="see-also"></a>另請參閱  
[複寫程式設計概念](../../relational-databases/replication/concepts/replication-programming-concepts.md)  
  
  
  
