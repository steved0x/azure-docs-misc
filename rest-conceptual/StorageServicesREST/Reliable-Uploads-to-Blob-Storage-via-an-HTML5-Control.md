---
title: "Reliable Uploads to Blob Storage via an HTML5 Control"
ms.custom: na
ms.date: 2016-06-29
ms.prod: azure
ms.reviewer: na
ms.service: storage
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 784f7cd6-480f-4c12-af5e-134f201af625
caps.latest.revision: 9
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
# Reliable Uploads to Blob Storage via an HTML5 Control
**Author:** Rahul Rai, Associate Consultant, Microsoft Global Delivery  
  
 **Source Code:** [http://code.msdn.microsoft.com/Silverlight-Azure-Blob-3b773e26](http://code.msdn.microsoft.com/Silverlight-Azure-Blob-3b773e26)  
  
## Summary  
 Use an HTML5 File API, AJAX and MVC 3 to build a robust file upload control to upload huge files securely and reliably to Azure blob storage with a provision of monitoring operation progress and operation cancellation.  
  
## Problem  
 Traditional file upload mechanisms lack client-side file processing capabilities and, therefore, cannot do chunked file uploads. Chunking file uploads gives you useful options, such as retrying to upload only the blocks that failed to reach the server, easy progress monitoring, and uploading large files.  
  
 HTML5 provides improvements in language and multimedia. We can now build a more fault tolerant and secure file upload control using the [HTML5 File API](http://www.w3.org/TR/file-upload/) and Azure block blob.  
  
## Solution  
 To build the file upload control, we need to develop three components:  
  
1.  Client-side JavaScript that accepts and processes a file uploaded by user.  
  
2.  Server-side code that processes file chunks sent by JavaScript.  
  
3.  Client-side UI that invokes JavaScript.  
  
### Implementation of Solution  
 **Prerequisites:**  
  
-   HTML5 supported browser (Internet Explorer 10+, FireFox 3.6+, or Google Chrome 7+)  
  
-   MVC 3  
  
-   JQuery  
  
-   Azure Storage API  
  
 To build this solution, use the following algorithm:  
  
1.  Accept a file from the user and check the browser’s capability of handling an HTML5 FileList.  
  
2.  Send metadata of the file, such as name of file, file size, number of blocks, etc., to the server in the form of JQuery **XmlHttpRequest**, and receive **JSON** response from the server. If the server has successfully saved this information, then start processing each file chunk.  
  
3.  Until the end of the file has been reached:  
  
    1.  Read 1 MB (configurable) slice of the file, attach an identifier to the request, and send it to the server with a block id (a sequentially generated number), where an **Action** method in the MVC controller accepts the HTML5 blob and uploads it as a block blob to Azure storage.  
  
    2.  Get a response in the form of a **JSON** message from the server and, upon success, process the next block. If the **JSON** message has data about failure of operation, render this data on the client and abort the operation.  
  
4.  If an error is encountered in sending the blob from JavaScript, hold the operation for 5 seconds (configurable) and retry the operation for the particular blob three more times (configurable). If the blob still fails to upload, then abort the operation.  
  
5.  If all the blobs successfully transmit to server, the `Action` method in MVC Controller commits the Azure blob by sending out the `Put Block List` request and sends the status of the operation to JavaScript as a **JSON** message.  
  
6.  At any time, you can cancel the operation and the system will force an exit from the routine by calling `abort()` on the handle attached to the current request in step 3a above.  
  
 The diagram below shows the steps in process:  
  
 ![HTML 5 Blob Upload process](../StorageServicesREST/media/HTML5BlobUpload_Process.gif "HTML5BlobUpload_Process")  
  
 Let’s now implement the solution by breaking down the algorithm in steps. Please note that trivial implementations have been left out for simplicity:  
  
1.  Accepting file from user and checking browser capabilities.  
  
    1.  Create an HTML5 supported MVC view with the following elements (high-level overview):  
  
        ```  
        <input type="file" id="FileInput" multiple="false"/>  
        <input type="button" id="upload" name="Upload" onclick="startUpload('FileInput', 1048576, 'uploadProgress', 'statusMessage', 'upload', 'cancel');" />  
        <input type="button" id="cancel" name="Cancel" onclick="cancelUpload();" class="button" />  
        ```  
  
    2.  Create a JavaScript file and implement `startUpload()` that is invoked from the **Upload** button. Click and test for browser compatibility for **FileList**. Also, because the enumeration object that we have is non-modifiable, it is a good practice to freeze such objects.  
  
        ```  
        function startUpload(fileElementId, blockLength, uploadProgressElement, statusLabel, uploadButton, cancelButton) {  
            Object.freeze(operationType);  
            uploader = Object.create(ChunkedUploader);  
            if (!window.FileList) {  
                uploader.statusLabel = document.getElementById(statusLabel);  
                uploader.displayLabel(operationType.UNSUPPORTED_BROWSER);  
                return;  
            }...  
        ```  
  
    3.  Design a prototype (as per ECMAScript5 guidelines) for `ChunkUpload` with all file knowledge encapsulated in it.  
  
        ```  
        var ChunkedUploader = {  
            constructor: function (controlElements) {  
                this.file = controlElements.fileControl.files[0];  
                this.fileControl = controlElements.fileControl;  
                this.statusLabel = controlElements.statusLabel;  
                this.progressElement = controlElements.progressElement;  
                this.uploadButton = controlElements.uploadButton;  
                this.cancelButton = controlElements.cancelButton;  
                this.totalBlocks = controlElements.totalBlocks;  
            },  
        ... /*UI functions omitted */  
        ```  
  
    4.  Create an instance from this prototype and initialize its data members from within `startUpload()`.  
  
        ```  
        function startUpload(fileElementId, blockLength, uploadProgressElement, statusLabel, uploadButton, cancelButton) {  
        ...  
        uploader = Object.create(ChunkedUploader);  
        ...  
            uploader.constructor({  
                "fileControl": document.getElementById(fileElementId),  
                "statusLabel": document.getElementById(statusLabel),  
                "progressElement": document.getElementById(uploadProgressElement),  
                "uploadButton": document.getElementById(uploadButton),  
                "cancelButton": document.getElementById(cancelButton),  
                "totalBlocks": 0  
            });  
        ...  
        }  
  
        ```  
  
2.  Send file metadata to server and save the information.  
  
    1.  Send file attributes as a **JSON** message to server and on receiving a success message, proceed with chunked upload.  
  
        ```  
        function startUpload(fileElementId, blockLength, uploadProgressElement, statusLabel, uploadButton, cancelButton) {  
        ...  
        $.ajax({  
                type: "POST",  
                async: true,  
                url: '/Home/PrepareMetaData',  
                data: {  
                    'blocksCount': uploader.totalBlocks,  
                    'fileName': uploader.file.name,  
                    'fileSize': uploader.file.size  
                },  
                dataType: "json",  
                error: function () {  
                    uploader.displayLabel(operationType.METADATA_FAILED);  
                    uploader.resetControls();  
                },  
                success: function (operationState) {  
                    if (operationState === true) {  
                        sendFile(blockLength);  
                    }  
                }  
            });  
        ...  
        }  
        ```  
  
    2.  Implement `PrepareMetadata Action` on **Home** controller.  
  
        ```  
        [HttpPost]  
                public ActionResult PrepareMetaData(int blocksCount, string fileName, long fileSize)  
                {  
                    var container = CloudStorageAccount.Parse(ConfigurationManager.AppSettings[Constants.ConfigurationSectionKey]).CreateCloudBlobClient().GetContainerReference(Constants.ContainerName);  
                    container.CreateIfNotExist();  
                    var fileToUpload = new FileUploadModel()  
                        {  
                            BlockCount = blocksCount,  
                            FileName = fileName,  
                            FileSize = fileSize,  
                            BlockBlob = container.GetBlockBlobReference(fileName),  
                            StartTime = DateTime.Now,  
                            IsUploadCompleted = false,  
                            UploadStatusMessage = string.Empty  
                        };  
                    Session.Add(Constants.FileAttributesSession, fileToUpload);  
                    return Json(true);  
                }  
        ```  
  
3.  Chunk uploading of file.  
  
    1.  Create a function that sends file chunks to server as **FormData** with an incremental chunk identifier. Do not use the **XMLHttpRequest** to directly send requests as Network Load Balancing (NLB) may strip off request headers making the chunk information meaningless. Note that currently the HTML5 slice function is implemented differently by different browsers, so the function is currently vendor prefixed.  
  
        -   For FireFox: `mozslice()`  
  
        -   For Chrome: `webkitslice()`  
  
        ```  
        var sendFile = function (blockLength) {  
        ...  
            sendNextChunk = function () {  
                fileChunk = new FormData();  
                uploader.renderProgress(incrimentalIdentifier);  
                if (uploader.file.slice) {  
                    fileChunk.append('Slice', uploader.file.slice(start, end));  
                }  
                else if (uploader.file.webkitSlice) {  
                    fileChunk.append('Slice', uploader.file.webkitSlice(start, end));  
                }  
                else if (uploader.file.mozSlice) {  
                    fileChunk.append('Slice', uploader.file.mozSlice(start, end));  
                }  
                else {  
                    uploader.displayLabel(operationType.UNSUPPORTED_BROWSER);  
                    return;  
                }  
                jqxhr = $.ajax({  
                    async: true,  
                    url: ('/Home/UploadBlock/' + incrimentalIdentifier),  
                    data: fileChunk,  
                    cache: false,  
                    contentType: false,  
                    processData: false,  
                    type: 'POST',  
                    error: function (request, error) { ...  
                    },  
                    success: function (notice) {  
                        ...  
                    }  
                });  
            };  
  
            sendNextChunk();  
        };  
        ```  
  
    2.  Implement an `UploadBlock` action in **Home** controller that takes incremental identifier as parameter, uploads the chunk and sends **JSON** message to the script indicating status of the operation. If the identifier increments until the last block, then commit all blocks by sending a `PutBlockList` request.  
  
        ```  
        [HttpPost]  
                [ValidateInput(false)]  
                public ActionResult UploadBlock(int id)  
                {  
                    byte[] chunk = new byte[Request.InputStream.Length];  
                    Request.InputStream.Read(chunk, 0, Convert.ToInt32(Request.InputStream.Length));  
                    if (Session[Constants.FileAttributesSession] != null)  
                    {  
                        var model = (FileUploadModel)Session[Constants.FileAttributesSession];  
                        using (var chunkStream = new MemoryStream(chunk))  
                        {  
                            var blockId = Convert.ToBase64String(Encoding.UTF8.GetBytes(string.Format(CultureInfo.InvariantCulture, "{0:D4}", id)));  
                            try  
                            {  
                                model.BlockBlob.PutBlock(blockId, chunkStream, null, new BlobRequestOptions() { RetryPolicy = RetryPolicies.Retry(3, TimeSpan.FromSeconds(10)) });  
                            }  
                            catch (StorageException e)  
                            {  
                                ...  
                                return Json(new { error = true, isLastBlock = false, message = model.UploadStatusMessage });  
                            }  
                        }  
  
                        if (id == model.BlockCount)  
                        {  
                            ...  
                            try  
                            {  
                                var blockList = Enumerable.Range(1, (int)model.BlockCount).ToList<int>().ConvertAll(rangeElement => Convert.ToBase64String(Encoding.UTF8.GetBytes(string.Format(CultureInfo.InvariantCulture, "{0:D4}", rangeElement))));  
                                model.BlockBlob.PutBlockList(blockList);  
                                ...  
                            }  
                            catch (StorageException e)  
                            {  
                                ...  
                            }  
                            finally  
                            {  
                                Session.Clear();  
                            }  
  
                            return Json(new { error = errorInOperation, isLastBlock = model.IsUploadCompleted, message = model.UploadStatusMessage });  
                        }  
                    }  
             else  
                    {  
                        return Json(new { error = true, isLastBlock = false, message = string.Format(Resources.FailedToUploadFileMessage, Resources.SessonExpired) });  
                    }  
  
                    return Json(new { error = false, isLastBlock = false, message = string.Empty });  
                }  
        ```  
  
4.  Recursively call the JavaScript function from success event handler of `JQueryXHR` in `sendNextChunk()` until end of file is reached. If an error is reported by server, then parse the **JSON** message and abort the operation. If the packet fails to reach the server (error event handler of `JQueryXHR`), then retry uploading the chunk with delays until you hit the maximum number of retries and then abort the operation.  
  
    ```  
    sendNextChunk = function () {  
            ...  
            jqxhr = $.ajax({  
                ...  
                error: function (request, error) {  
                    if (error !== 'abort' && retryCount < maxRetries) {  
                        ++retryCount;  
                        setTimeout(sendNextChunk, retryAfterSeconds * 1000);  
                    }  
  
                    if (error === 'abort') {  
                        ...  
                    }  
                    else {  
                        if (retryCount === maxRetries) {  
                            ...  
                        }  
                        else {  
                            uploader.displayLabel(operationType.RESUME_UPLOAD);  
                        }  
                    }  
  
                    return;  
                },  
                success: function (notice) {  
                    if (notice.error || notice.isLastBlock) {  
                        ...  
                        return;  
                    }  
  
                    ++incrimentalIdentifier;  
                    start = (incrimentalIdentifier - 1) * blockLength;  
                    end = Math.min(incrimentalIdentifier * blockLength, uploader.file.size) - 1;  
                    retryCount = 0;  
                    sendNextChunk();  
                }  
            });  
        };  
  
        sendNextChunk();  
    };  
    ```  
  
5.  If all incremental identifiers reach total block count, then the `UploadBlock` action in the **Home** controller will commit the blocks by sending a `PutBlockList` request.  
  
6.  To cancel the operation at any time, cancel the current AJAX request to which you have tied an identifier by calling `abort()` on the request.  
  
    ```  
    var sendFile = function (blockLength) {  
    ...  
            jqxhr = $.ajax({  
                ...  
                }  
            });  
        };  
  
    ...  
    };  
  
    cancelUpload = function () {  
        if (jqxhr !== null) {  
            jqxhr.abort();  
        }};  
    ```  
  
## Comparison between Silverlight version and HTML5 version of upload control  
 I wrote a field note about the [Silverlight version](http://www.microsoft.com/windowsazure/learn/real-world-guidance/field-notes/silverlight-azure-blob-parallel-upload/) of file upload control. Both the controls solve the issue of robust uploads through different approaches. The primary differences are summarized in the following table:  
  
|**Point of Difference**|**Silverlight Version**|**HTML5 Version**|  
|-----------------------------|-----------------------------|-----------------------|  
|**Browser dependence**|Runs on all browsers supporting Silverlight|Runs on lesser number of browsers as HTML5 standards are yet to be widely implemented|  
|**File upload mode**|Parallel|Sequential|  
|**Exposure of storage account keys**|SAS is exposed to the control|Has no knowledge of account keys|  
|**Time taken to render control**|High|Low|  
|**Component responsible for upload**|Client end control|Server handler|  
|**Failed block retries**|Supported at client end|Supported at client and server end|  
|**Client memory requirements**|High|Low|  
|**Time taken to upload file**|Low|High|  
|**Bandwidth utilization**|High|Low|  
|**File size supported**|Medium|High|  
  
## Future Scope  
  
1.  To make chunk uploads in parallel instead of the current sequential implementation, you may send out all **XmlHttpRequests** at one time instead of checking for successful delivery of each prenominal packet although this might clog the server if there is a high number of packets.  
  
2.  If AppFabric caching is used for maintaining metadata of file to upload, the control can easily scale out without requiring any modifications.  
  
3.  Support for multiple file upload may be added by carrying out the upload process for each file.  
  
## References  
  
-   **Slicing a file:** [http://www.html5rocks.com/en/tutorials/file/dndfiles/#toc-slicing-files](http://www.html5rocks.com/en/tutorials/file/dndfiles/)  
  
-   **Blob object:** [https://developer.mozilla.org/en/DOM/Blob](https://developer.mozilla.org/en/DOM/Blob)  
  
-   **ECMAScript Language Specification:** [http://www.ecma-international.org/publications/standards/Ecma-262.htm](http://www.ecma-international.org/publications/standards/Ecma-262.htm)  
  
-   **jQuery API:** [http://api.jquery.com/](http://api.jquery.com/)