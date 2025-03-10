---
title: "Download Table State"
manager: soliver
ms.date: 03/09/2015
ms.audience: Developer
ms.localizationpriority: medium
ms.assetid: 5bcc8b0a-0ab7-6c3e-8334-9e83cf2882a7
description: "Last modified: March 09, 2015"
 
 
---

# Download Table State

  
  
**Applies to**: Outlook 2013 | Outlook 2016 
  
 This topic describes what happens during the download table state of the replication state machine. 
  
## Quick info

|Property |Value |
|:-----|:-----|
|State Identifier:  <br/> |**LR_SYNC_DOWNLOAD_TABLE** <br/> |
|Related Data Structure:  <br/> |**[DNTBL](dntbl.md)** <br/> |
|From this state:  <br/> |[Synchronize contents state](synchronize-contents-state.md) <br/> |
|To this state:  <br/> |Synchronize contents state  <br/> |
   
> [!NOTE]
> The replication state machine is a deterministic state machine. A client departing from one state to another must eventually return to the former from the latter. 
  
## Description

This state initiates downloading a folder. During this state, Outlook initializes the associated **DNTBL** data structure with information about the folder. The client downloads the folder contents, and updates the folder on the local store with new contents, modifications, or deletions from the server. The download process adopts Microsoft Exchange Incremental Change Synchronization (ICS). For more information on ICS, see [ICS Evaluation Criteria](https://msdn.microsoft.com/library/aa579252%28EXCHG.80%29.aspx).
  
When this state ends, the local store returns to the synchronize contents state.
  
## See also



[About the Replication API](about-the-replication-api.md)
  
[MAPI Constants](mapi-constants.md)
  
[About the Replication State Machine](about-the-replication-state-machine.md)
  
[SYNCSTATE](syncstate.md)

