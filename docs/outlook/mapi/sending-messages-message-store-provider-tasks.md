---
title: "Sending Messages Message Store Provider Tasks"
manager: soliver
ms.date: 03/09/2015
ms.audience: Developer
ms.localizationpriority: medium
api_type:
- COM
ms.assetid: acbfd3ae-bfdc-4103-bed2-6bcf7b9c448c
description: "Last modified: March 09, 2015"
---

# Sending Messages: Message Store Provider Tasks

**Applies to**: Outlook 2013 | Outlook 2016 
  
A message store provider gets involved with the message sending process when a client calls the message's [IMessage::SubmitMessage](imessage-submitmessage.md) method. If multiple messages are to be sent, the message store must send them in the same order that the client used for its **SubmitMessage** calls. 
  
The message store provider determines whether or not to involve the MAPI spooler. If the message store provider is not tightly coupled, the message requires preprocessing, or the tightly coupled store and transport cannot handle all of the recipients, the MAPI spooler must be involved. 
  
The following procedure describes the tasks required of a message store provider for sending a message. 
  
**In IMessage::SubmitMessage, the message store provider**:
  
1. Calls [IMAPISupport::PrepareSubmit](imapisupport-preparesubmit.md) if the message has the MSGFLAG_RESEND flag set in its **PR_MESSAGE_FLAGS** ([PidTagMessageFlags](pidtagmessageflags-canonical-property.md)) property and returns any errors to the client. **PrepareSubmit** checks the **PR_RECIPIENT_TYPE** ([PidTagRecipientType](pidtagrecipienttype-canonical-property.md)) property of each recipient in the message's recipient list.
    
   - If the MAPI_SUBMITTED flag is set, indicating that the recipient did not receive the original message, **PrepareSubmit** clears the flag and sets the **PR_RESPONSIBILITY** ([PidTagResponsibility](pidtagresponsibility-canonical-property.md)) property to TRUE. 
    
   - If the MAPI_SUBMITTED flag is not set, indicating that the recipient did receive the original message, **PrepareSubmit** changes the **PR_RECIPIENT_TYPE** property to MAPI_P1 and sets the **PR_RESPONSIBILITY** property to TRUE and returns any error generated by **PrepareSubmit** to the client. 
    
2. Sets the MSGFLAG_SUBMIT flag in the message's **PR_MESSAGE_FLAGS** property. 
    
3. Makes sure that there is a column for **PR_RESPONSIBILITY** in the recipient table and sets it to FALSE to indicate that no transport has of yet assumed responsibility for transmitting the message. 
    
4. Sets the date and time of origination in the **PR_CLIENT_SUBMIT_TIME** ([PidTagClientSubmitTime](pidtagclientsubmittime-canonical-property.md)) property.
    
5. Calls [IMAPISupport::ExpandRecips](imapisupport-expandrecips.md) to: 
    
   - Expand all personal distribution lists and custom recipients and replace all changed display names with their original names.
   - Remove duplicate names.
   - Check for any required preprocessing, and if preprocessing is required, set the NEEDS_PREPROCESSING flag and the **PR_PREPROCESS** ([PidTagPreprocess](pidtagpreprocess-canonical-property.md)) property, a property reserved for MAPI. 
   - Set the NEEDS_SPOOLER flag if the message store is tightly coupled with a transport and it cannot handle all of the recipients. 
    
6. Performs the following tasks if the NEEDS_PREPROCESSING message flag is set:
    
   - Puts the message in the outgoing queue with the SUBMITFLAG_PREPROCESS bit set in the **PR_SUBMIT_FLAGS** ([PidTagSubmitFlags](pidtagsubmitflags-canonical-property.md)) property.
   - Notifies the MAPI spooler that the queue has changed.
   - Returns control to the client, and message flow continues in the MAPI spooler. 
   - The MAPI spooler performs the following tasks:
     - Locks the message by calling IMsgStore::SetLockState. 
     - Performs the needed preprocessing by calling all of the preprocessing functions in the order of registration. Transport providers call IMAPISupport::RegisterPreprocessor to register preprocessing functions. 
     - Calls IMessage::SubmitMessage on the open message to indicate to the message store that preprocessing is complete.


The following two steps occur in the client process if there was no preprocessing, and when the MAPI spooler calls **SubmitMessage** if there was preprocessing. 

**The message store provider**:

1. Performs the following tasks if the message store is tightly coupled to a transport and the NEEDS_SPOOLER flag was returned from [IMAPISupport::ExpandRecips](imapisupport-expandrecips.md):
    
   - Handles any recipients that it can handle.
   - Sets the **PR_RESPONSIBILITY** property to TRUE for any recipients that it handles. 
   - Performs the following tasks if all recipients are known to this tightly coupled store and transport:
     - Calls IMAPISupport::CompleteMsg if the message was preprocessed or the message store provider wants the MAPI spooler to complete message processing which is recommended so that messaging hooks can be invoked. Message flow continues with the MAPI spooler as described in the following procedure.  
     - Performs the following tasks if the message was not preprocessed or the message store provider does not want the MAPI spooler to complete message processing:
       - Copies the message to the folder identified by the entry identifier in the PR_SENTMAIL_ENTRYID (PidTagSentMailEntryId) property, if set.
       - Deletes the message if the PR_DELETE_AFTER_SUBMIT (PidTagDeleteAfterSubmit) property has been set to TRUE.
       - Unlocks the message if it is locked.
       - Returns to the client. Message flow is complete. 
   
2. Performs the following tasks if the message store is not tightly coupled to a transport, not all of the recipients were known to the message store, or the NEEDS_SPOOLER flag is set:
    
   - Puts the message in the outgoing queue without setting the SUBMITFLAG_PREPROCESS bit in the **PR_SUBMIT_FLAGS** property. 
   - Notifies the MAPI spooler that the outgoing queue has changed by generating a table notification. 
   - Returns to the client, and message flow continues with a set of tasks performed by the MAPI spooler.
    
When a message is to be handled by the MAPI spooler, the message store provider sets the message's **PR_SUBMIT_FLAGS** property to SUBMITFLAG_LOCKED. The SUBMITFLAG_LOCKED flag indicates that the MAPI spooler has locked the message for its exclusive use. The other value for **PR_SUBMIT_FLAGS,** SUBMITFLAG_PREPROCESS, is set when the message requires preprocessing by one or more preprocessor functions registered by a transport provider. 
  

