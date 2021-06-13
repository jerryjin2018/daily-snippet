### 1. Introduce AWS S3 presigned URL  
All objects by default are private. Only the object owner has permission to access these objects. However, the object owner can optionally share objects with others by creating a presigned URL, using their own security credentials, to grant time-limited permission to download the objects.

### 2. Python snippet  
```
import boto3
from botocore.exceptions import ClientError

# Notice
# Should configure your environment correctly, such as AWS AKSK or Role.

def main():

# "****newtestout" should be your bucket name
# "t**st/i***.png" is object name(or relative path and object name)

    client = boto3.client('s3')
    try:
        response = client.generate_presigned_url('get_object',
                                                  Params={'Bucket': "****newtestout",'Key': "t**st/i***.png"},
                                                  ExpiresIn=3600)
        print(response)
    except ClientError as e:
        print(e)

if __name__ == '__main__':
    main()   
```

### 3. Output for this snippet  
```
freeip:script host$ python ./create_preurl.py 
https://****newtestout.s3.cn-northwest-1.amazonaws.com.cn/t**st/i***.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZTGKYWNBM2VCDHDT%2F20210613%2Fcn-northwest-1%2Fs3%2Faws4_request&X-Amz-Date=20210613T053628Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Signature=ed2468e9509aa8b0e92193d3dd99980d30da1ff79633ccacd83a4109355b53fd
```

### 4. Quick way to get the presigned url for your object through AWS CLI  
```
freeip:script host$ aws s3 presign s3://****newtestout/*****logo.png --expires-in 604800
https://****newtestout.s3.cn-northwest-1.amazonaws.com.cn/*****logo.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAZTGKYWNBM2VCDHDT%2F20210613%2Fcn-northwest-1%2Fs3%2Faws4_request&X-Amz-Date=20210613T151807Z&X-Amz-Expires=604800&X-Amz-SignedHeaders=host&X-Amz-Signature=5182604605743b8617f5c5ac37fb3a9fe617377b9d56c2ee80d960621474460c
```
--expires-in (integer) Number of seconds until the pre-signed URL expires. Default is 3600 seconds, and 604800 for one week.

### 5. Reference
[https://boto3.amazonaws.com/v1/documentation/api/1.11.4/guide/s3-presigned-urls.html](https://boto3.amazonaws.com/v1/documentation/api/1.11.4/guide/s3-presigned-urls.html)
[https://docs.aws.amazon.com/cli/latest/reference/s3/presign.html](https://docs.aws.amazon.com/cli/latest/reference/s3/presign.html)
