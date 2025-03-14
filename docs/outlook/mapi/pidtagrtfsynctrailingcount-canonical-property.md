---
title: "PidTagRtfSyncTrailingCount Canonical Property"
 
 
manager: soliver
ms.date: 03/09/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
ms.localizationpriority: medium
api_name:
- MAPI.PidTagRtfSyncTrailingCount
api_type:
- COM
ms.assetid: 3f0e5b24-767e-46f5-bb3d-e9cb82cb935b
description: "Contains a count of the ignorable characters that appear after the significant characters of the message."
---

# PidTagRtfSyncTrailingCount Canonical Property

  
  
**Applies to**: Outlook 2013 | Outlook 2016 
  
Contains a count of the ignorable characters that appear after the significant characters of the message.
  
|Property |Value |
|:-----|:-----|
|Associated properties:  <br/> |PR_RTF_SYNC_TRAILING_COUNT  <br/> |
|Identifier:  <br/> |0x1011  <br/> |
|Data type:  <br/> |PT_LONG  <br/> |
|Area:  <br/> |MAPI message  <br/> |
   
## Remarks

This property is a Rich Text Format (RFT) auxiliary property. These properties are used by the [RTFSync](rtfsync.md) function and are not intended to be used directly by client applications. 
  
## Related resources

### Protocol specifications

[[MS-OXPROPS]](https://msdn.microsoft.com/library/f6ab1613-aefe-447d-a49c-18217230b148%28Office.15%29.aspx)
  
> Provides references to related Exchange Server protocol specifications.
    
[[MS-OXTNEF]](https://msdn.microsoft.com/library/1f0544d7-30b7-4194-b58f-adc82f3763bb%28Office.15%29.aspx)
  
> Encodes and decodes message and attachment objects to an efficient stream representation.
    
### Header files

Mapidefs.h
  
> Provides data type definitions.
    
Mapitags.h
  
> Contains definitions of properties listed as alternate names.
    
## See also



[MAPI Properties](mapi-properties.md)
  
[MAPI Canonical Properties](mapi-canonical-properties.md)
  
[Mapping Canonical Property Names to MAPI Names](mapping-canonical-property-names-to-mapi-names.md)
  
[Mapping MAPI Names to Canonical Property Names](mapping-mapi-names-to-canonical-property-names.md)

