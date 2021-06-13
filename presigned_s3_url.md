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

### 4. Reference
[https://boto3.amazonaws.com/v1/documentation/api/1.11.4/guide/s3-presigned-urls.html](url)
