---
title: "Blob Service Error Codes"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: a3c7e7f9-91c3-4550-8825-2e96a83fd99e
caps.latest.revision: 29
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
# Blob Service Error Codes
The error codes listed in the following table may be returned by an operation against the Blob service.  
  
|Error code|HTTP status code|User message|  
|----------------|----------------------|------------------|  
|InvalidBlobOrBlock|Bad Request (400)|The specified blob or block content is invalid.|  
|InvalidBlockId|Bad Request (400)|The specified block ID is invalid. The block ID must be Base64-encoded.|  
|InvalidBlockList|Bad Request (400)|The specified block list is invalid.|  
|ContainerNotFound|Not Found (404)|The specified container does not exist.|  
|BlobNotFound|Not Found (404)|The specified blob does not exist.|  
|ContainerAlreadyExists|Conflict (409)|The specified container already exists.|  
|ContainerDisabled|Conflict (409)|The specified container has been disabled by the administrator.|  
|ContainerBeingDeleted|Conflict (409)|The specified container is being deleted.|  
|BlobAlreadyExists|Conflict (409)|The specified blob already exists.|  
|BlockCountExceedsLimit|Conflict (409)|The committed block count exceeds the maximum permissible limit.|  
|InvalidBlobType|Conflict (409)|The blob type is invalid for this operation.|  
|LeaseNotPresentWithBlobOperation|Precondition Failed (412)|There is currently no lease on the blob.|  
|LeaseNotPresentWithContainerOperation|Precondition Failed (412)|There is currently no lease on the container.|  
|LeaseLost|Precondition Failed (412)|A lease ID was specified, but the lease for the blob/container has expired.|  
|LeaseIdMismatchWithBlobOperation|Precondition Failed (412)|The lease ID specified did not match the lease ID for the blob.|  
|LeaseIdMismatchWithContainerOperation|Precondition Failed (412)|The lease ID specified did not match the lease ID for the container.|  
|LeaseIdMissing|Precondition Failed (412)|There is currently a lease on the blob/container and no lease ID was specified in the request.|  
|MaxBlobSizeConditionNotMet|Precondition Failed (412)|The max blob size condition specified was not met.|  
|AppendPositionConditionNotMet|Precondition Failed (412)|The append position condition specified was not met.|  
|LeaseNotPresentWithLeaseOperation|Conflict (409)|There is currently no lease on the blob/container.|  
|LeaseIdMismatchWithLeaseOperation|Conflict (409)|The lease ID specified did not match the lease ID for the blob/container.|  
|LeaseAlreadyPresent|Conflict (409)|There is already a lease present.|  
|LeaseAlreadyBroken|Conflict (409)|The lease has already been broken and cannot be broken again.|  
|LeaseIsBrokenAndCannotBeRenewed|Conflict (409)|The lease ID matched, but the lease has been broken explicitly and cannot be renewed.|  
|LeaseIsBreakingAndCannotBeAcquired|Conflict (409)|The lease ID matched, but the lease is currently in breaking state and cannot be acquired until it is broken.|  
|LeaseIsBreakingAndCannotBeChanged|Conflict (409)|The lease ID matched, but the lease is currently in breaking state and cannot be changed.|  
|InfiniteLeaseDurationRequired|Precondition Failed (412)|The lease ID matched, but the specified lease must be an infinite-duration lease.|  
|SnapshotsPresent|Conflict (409)|This operation is not permitted because the blob has snapshots.|  
|InvalidBlobType|Conflict (409)|The blob type is invalid for this operation.|  
|FeatureVersionMismatch|Conflict (409)|The operation for AppendBlob requires at least version 2015-02-21.|  
|FeatureVersionMismatch|Conflict (409)|The type of blob in the container is unrecognized by this version.|  
|InvalidVersionForPageBlobOperation|Bad Request (400)|All operations on page blobs require at least version 2009-09-19.|  
|InvalidPageRange|Requested Range Not Satisfiable (416)|The page range specified is invalid.|  
|SequenceNumberConditionNotMet|Precondition Failed (412)|The sequence number condition specified was not met.|  
|SequenceNumberIncrementTooLarge|Conflict (409)|The sequence number increment cannot be performed because it would result in overflow of the sequence number.|  
|SourceConditionNotMet|Precondition Failed (412)|The source condition specified using HTTP conditional header(s) is not met.|  
|TargetConditionNotMet|Precondition Failed (412)|The target condition specified using HTTP conditional header(s) is not met.|  
|CopyAcrossAccountsNotSupported|Bad Request (400)|The copy source account and destination account must be the same.|  
|CannotVerifyCopySource|Internal Server Error (500)|Could not verify the copy source within the specified time. Examine the HTTP status code and message for more information about the failure.|  
|PendingCopyOperation|Conflict (409)|There is currently a pending copy operation.|  
|NoPendingCopyOperation|Conflict (409)|There is currently no pending copy operation.|  
|CopyIdMismatch|Conflict (409)|The specified copy ID did not match the copy ID for the pending copy operation.|  
|SnapshotCountExceeded|Conflict (409)|The snapshot count against this blob has been exceeded.|  
|SnaphotOperationRateExceeded|Conflict (409)|The rate of snapshot operations against this blob has been exceeded.|  
|InvalidOperation|Bad Request (400)|Invalid operation against a blob snapshot.|  
|SnapshotsPresent|Conflict (409)|This operation is not permitted while the blob has snapshots.|  
|UnsupportedHeader|Bad Request (400)|One of the headers specified in the request is not supported.|  
|SystemInUse|Conflict (409)|This blob is in use by the system.|  
|PreviousSnapshotNotFound|Conflict (409)|The previous snapshot is not found.|  
|PreviousSnapshotOperationNotSupported|Conflict (409)|Differential [Get Page Ranges](../StorageServicesREST/Get-Page-Ranges.md) is not supported on the previous snapshot.|  
|BlobGenerationMismatch|Conflict (409)|The previous snapshot is from a different blob generation.|  
|PreviousSnapshotCannotBeNewer|Bad Request (400)|The `prevsnapshot` query parameter value cannot be newer than snapshot query parameter value.|  
  
## See Also  
 [Common REST API Error Codes](../StorageServicesREST/Common-REST-API-Error-Codes.md)   
 [Queue Service Error Codes](../StorageServicesREST/Queue-Service-Error-Codes.md)   
 [Table Service Error Codes](../StorageServicesREST/Table-Service-Error-Codes.md)   
 [Troubleshooting API Operations](../StorageServicesREST/Troubleshooting-API-Operations.md)   
 [HttpStatusCode Enumeration](http://go.microsoft.com/fwlink/?LinkId=152845)   
 [Storage Services REST](../StorageServicesREST/Azure-Storage-Services-REST-API-Reference.md)