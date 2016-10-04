---
title: "Features Not Supported By the Azure File Service"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 543f0f3c-88d3-4591-8b19-5caa94d6167f
caps.latest.revision: 6
author: tamram
manager: carolz
translation.priority.mt: 
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pt-br
  - ru-ru
  - zh-cn
  - zh-tw
---
# Features Not Supported By the Azure File Service
The Microsoft Azure File service supports a subset of the SMB 3.0 and 2.1 protocols. The majority of applications do not use the SMB features that are not supported by the File service, so most applications will work as designed when using files stored in the File service. However, some applications may not work properly with the File service if they rely on these unsupported features. The following is a list of the SMB features that are not supported by the File service:  
  
-   [SMB Multichannel](http://blogs.technet.com/b/josebda/archive/2012/05/13/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0.aspx)  
  
-   [SMB Direct](https://technet.microsoft.com/en-us/library/jj134210.aspx)  
  
-   [SMB Directory Leasing](https://technet.microsoft.com/en-us/library/hh831795.aspx)  
  
-   [Volume Shadow Copy Service for SMB file share](http://blogs.technet.com/b/clausjor/archive/2012/06/14/vss-for-smb-file-shares.aspx)  
  
-   [Alternate data streams](http://msdn.microsoft.com/library/windows/desktop/aa364404\(v=vs.85\).aspx)  
  
-   [Extended attributes](http://en.wikipedia.org/wiki/Extended_file_attributes)  
  
-   [Security descriptors](http://msdn.microsoft.com/library/windows/hardware/ff556612\(v=vs.85\).aspx)  
  
-   [Object identifiers](http://msdn.microsoft.com/library/windows/desktop/aa363997\(v=vs.85\).aspx)  
  
-   [Hard links](http://msdn.microsoft.com/library/windows/desktop/aa365006\(v=vs.85\).aspx)  
  
-   [Soft links](http://msdn.microsoft.com/library/windows/desktop/aa363878\(v=vs.85\).aspx)  
  
-   [Reparse points](http://msdn.microsoft.com/library/windows/desktop/aa365503\(v=vs.85\).aspx)  
  
-   [Sparse files](http://msdn.microsoft.com/library/windows/desktop/aa365564\(v=vs.85\).aspx)  
  
-   [Short file names (8.3 alias)](http://support.microsoft.com/kb/142982)  
  
-   [Compression](http://msdn.microsoft.com/library/windows/desktop/aa364592\(v=vs.85\).aspx)  
  
-   [Named pipes](http://msdn.microsoft.com/library/windows/desktop/aa365590\(v=vs.85\).aspx)  
  
-   [Server service](http://technet.microsoft.com/library/cc958790.aspx)  
  
-   [File system transactions (TxF)](http://msdn.microsoft.com/magazine/cc163388.aspx)  
  
## See Also  
 [File Service REST API](../StorageServicesREST/File-Service-REST-API.md)