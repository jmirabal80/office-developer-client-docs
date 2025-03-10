---
title: "MAPIERROR"
 
 
manager: soliver
ms.date: 03/09/2015
ms.audience: Developer
ms.topic: reference
ms.prod: office-online-server
ms.localizationpriority: medium
api_name:
- MAPI.MAPIERROR
api_type:
- COM
ms.assetid: e04c2228-aa0a-4958-b5b2-6467e93ab613
description: "Last modified: March 09, 2015"
---

# MAPIERROR

  
  
**Applies to**: Outlook 2013 | Outlook 2016 
  
Provides detailed information about an error, typically generated by the operating system, MAPI, or a service provider. 
  
|Property|Value|
|:-----|:-----|
|Header file:  <br/> |Mapidefs.h  <br/> |
   
```cpp
typedef struct _MAPIERROR
{
  ULONG ulVersion;
  LPSTR lpszError;
  LPSTR lpszComponent;
  ULONG ulLowLevelError;
  ULONG ulContext;
} MAPIERROR, FAR * LPMAPIERROR;

```

## Members

 **ulVersion**
  
> Version number of the structure. The **ulVersion** member is used for future expansion and should be set to MAPI_ERROR_VERSION, which is currently defined as zero. 
    
 **lpszError**
  
> Pointer to a string that describes the error. This string will be in Unicode format if the _ulFlags_ parameter to the method in which this structure is used is set to MAPI_UNICODE. 
    
 **lpszComponent**
  
> Pointer to a string that describes the component that generated the error. This string will be in Unicode format if the _ulFlags_ parameter to the method in which this structure is used is set to MAPI_UNICODE. 
    
 **ulLowLevelError**
  
> Low-level error value that is used only when the error to be returned is low-level.
    
 **ulContext**
  
> Value that represents the location in the component pointed to by the **lpszComponent** member that identifies where the error occurred. 
    
## Remarks

The **MAPIERROR** structure is used to describe error information. Clients and service providers pass a pointer to a **MAPIERROR** structure in the _lppMAPIError_ parameter of the [IMAPIProp::GetLastError](imapiprop-getlasterror.md) method. **GetLastError** returns information about the previous error that has occurred to an object. Callers of **GetLastError** free the memory for the **MAPIERROR** structure by calling [MAPIFreeBuffer](mapifreebuffer.md).
  
The **lpszComponent** member can be used to map the component's Help file, if one exists. Service providers should limit the size of the component string to 30 characters so that it can easily be displayed in a dialog box. The **ulContext** member can also be used to refer to an online Help topic for common errors. 
  
Because service providers are not required to provide detailed error information, clients should not expect any of the members of the **MAPIERROR** structure that are returned to contain valid data. However, at a minimum MAPI strongly recommends that providers specify information in the **lpszComponent** and **ulContext** members. 
  
For more information about error handling in MAPI, see [Error Handling](error-handling-in-mapi.md).
  
## See also



[IABLogon::GetLastError](iablogon-getlasterror.md)
  
[IABProvider::Logon](iabprovider-logon.md)
  
[IMAPIControl::GetLastError](imapicontrol-getlasterror.md)
  
[IMAPIProp::GetLastError](imapiprop-getlasterror.md)
  
[IMAPISession::GetLastError](imapisession-getlasterror.md)
  
[IMAPISupport::GetLastError](imapisupport-getlasterror.md)
  
[IMAPISupport::OpenAddressBook](imapisupport-openaddressbook.md)
  
[IMAPISession::OpenAddressBook](imapisession-openaddressbook.md)
  
[IMAPITable::GetLastError](imapitable-getlasterror.md)
  
[IMsgServiceAdmin::GetLastError](imsgserviceadmin-getlasterror.md)
  
[IMSLogon::GetLastError](imslogon-getlasterror.md)
  
[IMSProvider::Logon](imsprovider-logon.md)
  
[IProfAdmin::GetLastError](iprofadmin-getlasterror.md)
  
[IProviderAdmin::GetLastError](iprovideradmin-getlasterror.md)


[MAPI Structures](mapi-structures.md)

