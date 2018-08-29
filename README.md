# Step Functions With Long Asynchronous Activities

## TL;DR
Example for using long-running asynchronous activities with AWS Step Functions.

## Background
Step functions steps can be a Lambda function directly, or they can be an *Activity*. One of the advantages of activities is the ability to perform long-running tasks. The state machine will hold an execution and wait for an update from the *worker* who polled and now executes the task. The update signals the end of this step of the execution, and can be with either success or failure status.

## Video Ingest Use Case Sample
For demonstrating this, we will use a video ingestion workflow. This automated flow will detect a video file upload to a designated S3 bucket, and trigger a process that uses Amazon Rekognition to check if the video is safe.
High level architecture:

<p align="center">
<img src="https://github.com/moshesaws/step-functions-activity/blob/master/arch.png">
</p>

## Deploy and Test

* Create a new stack in your AWS account under CloudFormation with the provided yaml file of this repo.
* Upload an .mp4 video file to the "RawVideoSourceBucket" bucket.
* From the AWS console open the Step Functions dashboard, and check the state machine execution.
* If the execution was successfull, check the "approved" bucket - your video should be copied there!


## Disclaimer
The samples in this repository are meant to help users understand the concept of activities in Step Functions. They are not sufficient for production environments. Users should carefully inspect samples before running and/or using them.

Use at your own risk.

## Built With

* [AWS](https://aws.amazon.com/) - Amazon Web Services
* [CloudFormation](https://aws.amazon.com/cloudformation/) - Model and set up your Amazon Web Services resources


