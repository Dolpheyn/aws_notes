- #aws #cloud #notes
- AWS Build On

**Table of Contents**
1. [IAM Credentials](#IAM-Credentials)
2. [AWS SDK for javascript](#AWS-SDK-for-javascript)
3. [SageMaker](#SageMaker)


# IAM Credentials
https://console.aws.amazon.com/iam/home?#/security_credentials  

# AWS SDK for javascript

- **Installing the SDK for JavaScript**
```shell
npm install aws-sdk
```

- **Store creds on shared file**  
https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/loading-node-credentials-shared.html  
The shared credentials file on Linux, Unix, and macOS: `~/.aws/credentials`  
e.g.  
  
```toml
[any-name]
aws_access_key_id = <DEFAULT_ACCESS_KEY_ID>
aws_secret_access_key = <DEFAULT_SECRET_ACCESS_KEY>
```

- **Load sdk and connect to an S3 instance**
```js
// Load the AWS SDK for Node.js
var AWS = require('aws-sdk');

// Load shared credentials
var credentials = new AWS.SharedIniFileCredentials({profile: 'any-name'});
AWS.config.credentials = credentials;

// Set the region 
AWS.config.update({region: 'REGION'});

// Create S3 service object
s3 = new AWS.S3({apiVersion: '2006-03-01'});

// Call S3 to list the buckets
s3.listBuckets(function(err, data) {
  if (err) {
    console.log("Error", err);
  } else {
    console.log("Success", data.Buckets);
  }
});
```
# SageMaker
- Wtf is Object Artifacts?
- Kena sambung git with notebook instance ke?
- Definitely using BYO Algorithm.
