# 如何进行分段上传？\(Java SDK\)<a name="obs_21_2114"></a>

在上传文件时，您可以指定上传文件的某一段的数据来进行分段上传，步骤如下：

1.  您需要以AK、SK、Endpoint先初始化一个客户端ObsClient；
2.  指定桶名和对象名初始化一个InitiateMultipartUploadRequest，您可以通过InitiateMultipartUploadRequest.setMetadata接口设置将要上传的对象的元数据信息，然后通过ObsClient.initiateMultipartUpload接口初始化一个分段上传任务，这个接口会返回一个全局唯一标示（Upload ID），用于标识本次分段上传任务；
3.  指定桶名和对象名初始化一个UploadPartRequest请求，通过UploadPartRequest.setUploadId接口设置该上传段所属的uploadId，setPartNumber接口设置该上传段的段号，setFile接口设置该上传段所属的将要上传的大文件，setPartSize接口设置该上传段的段大小；然后通过ObsClient.uploadPart接口上传该段，这个接口会返回该上传段的ETag值；
4.  在所有分段上传完成后，指定桶名、对象名、uploadId、partEtags来初始化一个CompleteMultipartUploadRequest请求，然后通过ObsClient.completeMultipartUpload接口进行合并段操作。

详细操作可参见[分段上传](分段上传(Java-SDK).md)。

