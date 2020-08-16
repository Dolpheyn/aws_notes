- #aws #cloud #notes
- AWS Build On

**Table of Contents**
1. [IAM Credentials](#IAM-Credentials)
2. [AWS SDK for javascript](#AWS-SDK-for-javascript)
3. [SageMaker](#SageMaker)
	1. [Steps for ML With SageMaker](#Steps-For-ML-wih-SageMaker)


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
https://docs.aws.amazon.com/sagemaker/index.html
   
- Wtf is Object Artifacts?:
	- A: Maybe *Model Artifacts* in the pic at [Steps For ML wih SageMaker](#Steps-For-ML-wih-SageMaker)(?)
- Kena sambung git with notebook instance ke?
- Definitely using BYO Algorithm.
- **SageMaker Notebook**:
	- Host Jupter notebook to:
		- Preprocess data
		- Write code to create model training jobs
		- Deploy models to Amazon Sagemaker hosting
		- Test of validate models
- **SageMaker Processing**:
	- Automate pre- and post- process data.
	- Feature engineering(?)
	- Evaluate models(?)
  
## Steps For ML wih SageMaker
----
[sagemaker architecture png](./imgs/sagemaker-architecture.png.md)
  \
1. Preprocess data:
	1. Manual - SageMaker Notebook (**use this option first.**)
	2. Automatic - SageMaker Processing:
		1. [Processing job using scikit learn](https://docs.aws.amazon.com/sagemaker/latest/dg/processing-job.html)
2. Model Training:
	1. Create a training job. It includes:
		1. S3 URL (training data)
		2. Compute Instances(?):
		3. SR URL (output of the job which are  model artifacts.) rasanya boleh je store in the same
		   bucket with training data.
		4. Read options for training at https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-training.html
		5. Answer for no. 2 ^^^:
			1. "After you create the training job, Amazon SageMaker launches the ML compute instances
			   and uses the training code and the training dataset to train the model.  It saves the
			   resulting model artifacts and other output in the S3 bucket you specified for that
			   purpose."
			2. > Compute instances dia auto launch.
		6. [Read more](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-training.html)
3. Model depolyment:
	1. [Read](https://docs.aws.amazon.com/sagemaker/latest/dg/how-it-works-deployment.html)
	2. [Example](https://docs.aws.amazon.com/sagemaker/latest/dg/ex1-deploy-model.html)



