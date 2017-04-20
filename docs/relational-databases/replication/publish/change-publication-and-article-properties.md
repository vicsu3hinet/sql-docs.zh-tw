---
title: "變更發行集與發行項屬性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "修改發行項屬性"
  - "修改發行集屬性"
  - "管理複寫, 屬性"
  - "發行集 [SQL Server 複寫], 變更屬性"
  - "發行項 [SQL Server 複寫], 屬性"
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 變更發行集與發行項屬性
  在建立發行集後，可以變更大多數發行集與發行項屬性，但某些屬性要求重新產生快照集和 (或) 重新初始化訂閱。 本主題提供在變更時需要執行一個或兩個動作的所有屬性之資訊。  
  
## 快照式和異動複寫的發行集屬性  
  
|描述|預存程序|屬性|需求|  
|-----------------|----------------------|----------------|------------------|  
|變更快照集格式。|**sp_changepublication**|**sync_method**|新的快照集。|  
|變更快照集位置。|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|新的快照集。|  
|變更快照集位置。|**sp_changedistpublisher**|**working_directory**|新的快照集。|  
|變更快照集壓縮。|**sp_changepublication**|**compress_snapshot**|新的快照集。|  
|變更任何「檔案傳輸通訊協定」(FTP) 快照集選項。|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|新的快照集。|  
|變更前快照集或後快照集指令碼位置。|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|新的快照集 (如果您變更指令碼內容，也需要這項)。<br /><br /> 將新的指令碼套用至訂閱者需要重新初始化。|  
|啟用或停用支援非[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 「 訂閱者 」。|**sp_changepublication**|**is_enabled_for_het_sub**|新的快照集。|  
|變更佇列更新訂閱的衝突報告|**sp_changepublication**|**centralized_conflicts**|只有沒有使用中的訂閱時，才能變更。|  
|變更佇列更新訂閱的衝突解決原則。|**sp_changepublication**|**conflict_policy**|只有沒有使用中的訂閱時，才能變更。|  
  
## 快照式和異動複寫的發行項屬性  
  
|描述|預存程序|屬性|需求|  
|-----------------|----------------------|----------------|------------------|  
|卸除發行項|**sp_droparticle**|所有參數。|可以在建立訂閱之前卸除發行項。 使用預存程序，可以卸除發行項訂閱；使用 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]，必須卸除、重新建立並同步處理整個訂閱。 如需詳細資訊，請參閱 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。|  
|變更資料行篩選。|**sp_articlecolumn**|**@column**<br /><br /> **@operation**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|新增資料列篩選。|**sp_articlefilter**|所有參數。|新的快照集。<br /><br /> 重新初始化訂閱。|  
|卸除資料列篩選。|**sp_articlefilter**|**@article**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更資料列篩選。|**sp_articlefilter**|**@filter_clause**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更資料列篩選。|**sp_changearticle**|**filter**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更結構描述選項。|**sp_changearticle**|**schema_option**|新的快照集。|  
|在套用快照集之前，變更在「訂閱者」端處理資料表的方式。|**sp_changearticle**|**pre_creation_cmd**|新的快照集。|  
|變更發行項狀態|**sp_changearticle**|**status**|新的快照集。|  
|變更 INSERT、UPDATE 或 DELETE 命令。|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更目的地資料表名稱|**sp_changearticle**|**dest_table**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更目的地資料表擁有者 (結構描述)。|**sp_changearticle**|**destination_owner**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更資料類型對應 (僅套用至 Oracle 發行)。|**sp_changearticlecolumndatatype**|**@type**<br /><br /> **@length**<br /><br /> **@precision**<br /><br /> **@scale**|新的快照集。<br /><br /> 重新初始化訂閱。|  
  
## 合併式複寫的發行集屬性  
  
|描述|預存程序|屬性|需求|  
|-----------------|----------------------|----------------|------------------|  
|變更快照集格式|**sp_changemergepublication**|**sync_mode**|新的快照集。|  
|變更快照集位置。|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|新的快照集。|  
|變更快照集位置。|**sp_changedistpublisher**|**working_directory**|新的快照集。|  
|變更快照集壓縮|**sp_changemergepublication**|**compress_snapshot**|新的快照集。|  
|變更任何 FTP 快照集選項|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|新的快照集。|  
|變更前快照集或後快照集指令碼。|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|新的快照集 (如果您變更指令碼內容，也需要這項)。<br /><br /> 將新的指令碼套用至訂閱者需要重新初始化。|  
|新增聯結篩選或邏輯記錄。|**sp_addmergefilter**|所有參數。|新的快照集。<br /><br /> 重新初始化訂閱。|  
|卸除聯結篩選或邏輯記錄。|**sp_dropmergefilter**|所有參數。|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更聯結篩選或邏輯記錄。|**sp_changemergefilter**|**@property**<br /><br /> **@value**|新增快照集<br /><br /> 重新初始化訂閱。|  
|停用參數化篩選 (啟用參數化篩選不需要執行任何特殊動作)。|**sp_changemergepublication**|值為 **false** 的 **dynamic_filters**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|啟用或停用預先計算的資料分割。|**sp_changemergepublication**|**use_partition_groups**|新的快照集。|  
|啟用或停用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 資料分割最佳化。|**sp_changemergepublication**|**keep_partition_changes**|重新初始化訂閱。|  
|啟用或停用「訂閱者」資料分割驗證。|**sp_changemergepublication**|**validate_subscriber_info**|重新初始化訂閱。|  
|將發行集相容性層級變更為 80sp3 或更低。|**sp_changemergepublication**|**publication_compatibility_level**|新的快照集。|  
  
## 合併式複寫的發行項屬性  
  
|描述|預存程序|屬性|需求|  
|-----------------|----------------------|----------------|------------------|  
|卸除發行項，其中發行項在發行集中具有最終參數化篩選。|**sp_dropmergearticle**|所有參數|新的快照集。<br /><br /> 重新初始化訂閱。|  
|卸除發行項，其中發行項是聯結篩選或邏輯記錄中的父系 (這會有卸除聯結的副作用)。|**sp_dropmergearticle**|所有參數|新的快照集。<br /><br /> 重新初始化訂閱。|  
|卸除發行項，所有其他情形。|**sp_dropmergearticle**|所有參數|新的快照集。|  
|包括先前未發行的資料行篩選。|**sp_mergearticlecolumn**|**@column**<br /><br /> **@operation**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|新增、卸除或變更資料列篩選。|**sp_changemergearticle**|**subset_filterclause**|新的快照集。<br /><br /> 重新初始化訂閱。<br /><br /> 如果您新增、卸除或變更參數化篩選，在重新初始化期間，便無法將訂閱者的暫止變更上傳到發行者。 如果您要上傳暫止變更，請在變更篩選之前，同步處理所有訂閱。<br /><br /> 如果發行項與所有聯結篩選無關，您可以卸除發行項，然後再使用不同的資料列篩選將其新增，這並不需要重新初始化整個訂閱。 如需加入和卸除發行項的詳細資訊，請參閱 [新增和卸除現有的發行集的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。|  
|變更結構描述選項。|**sp_changemergearticle**|**schema_option**|新的快照集。|  
|將追蹤從資料行層級變更為資料列層級 (從資料列層級追蹤變更為資料行追蹤不需要執行任何特殊動作)。|**sp_changemergearticle**|值為 **false** 的 **column_tracking**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|變更在將「訂閱者」端所進行的陳述式套用至「發行者」之前是否要檢查權限。|**sp_changemergearticle**|**check_permissions**|新的快照集。<br /><br /> 重新初始化訂閱。|  
|啟用或停用僅限下載的訂閱 (與其他上傳選項相關的變更不需要執行任何特殊動作)。|**sp_changemergearticle**|值變更 **2** 的 **subscriber_upload_options**|重新初始化訂閱。|  
|變更目的地資料表擁有者。|**sp_changemergearticle**|**destination_owner**|新的快照集。<br /><br /> 重新初始化訂閱。|  
  
## 另請參閱  
 [管理 & #40。複寫 & #41;](../../../relational-databases/replication/administration/administration-replication.md)   
 [建立並套用快照集](../../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [重新初始化訂閱](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [sp_addmergefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_articlecolumn & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sp_articlefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_changearticlecolumndatatype & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)   
 [sp_changedistpublisher & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_changemergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_changemergefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_changemergepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_changepublication & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droparticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_dropmergearticle & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_dropmergefilter & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_mergearticlecolumn & #40。TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md)  
  
  