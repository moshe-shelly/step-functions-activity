# Step Functions With Long Asynchronous Activities

## TL;DR
Example for using long-running asynchronous activities with AWS Step Functions.

## Background
Step functions can orchestrate Lambda function directly, and can also use an *Activity* - a step whose actual work gets done externally. One of the advantages of activities is the ability to perform long-running tasks. The state machine will hold its execution and wait for an update from the *worker* who polled and now executes the activity's task. The worker signals the end of this *activity* step, with either success or failure status.

## Video Ingest Use Case Sample
For demonstrating this, we will use a video ingestion workflow. This automated flow will detect a video file upload to a designated S3 bucket, and trigger a process that uses Amazon Rekognition to check if the video is safe.
High level architecture:

<p align="center">
<img src="https://github.com/moshesaws/step-functions-activity/blob/master/arch.png">
</p>


What happens here?
1. You upload a file to the *Raw* bucket
2. The bucket is configured to send events when an object is created, which triggers a Lambda function (via an SNS topic, not shown in diagram for simplicity)
3. The lambda function starts an *execution* of the Step Function's state machine

In parallel, we have a CloudWatch schedule rule, that **polls** our state machine for work on a 1-minute interval. When system is idle, no tasks are avaialble. But after a file upload, a task is available. What happens now is:
1. The Lambda function gets the details about the new video file from the newly available task, _and stores the task ID_
2. It triggers an asynchronous request to Rekognition, to detect if the content is safe (Content Moderation)
3. The async response from Rekognition returns via SNS, to trigger the third (and final) Lambda function, which _signals our state machine about the end of this task_


## Deploy and Test

* Create a new stack in your AWS account under CloudFormation with the provided yaml file of this repo.
* Upload an .mp4 video file to the "RawVideoSourceBucket" bucket.
* From the AWS console open the Step Functions dashboard, and check the state machine execution.
* If the execution was successfull, check the "approved" bucket - your video should be copied there!


## Disclaimer
The samples in this repository are meant to help users understand the concept of activities in Step Functions. They are not sufficient for production environments. Users should carefully inspect samples before running and/or using them.

Use at your own risk.

## Built With

* [AWS Step Functions](https://aws.amazon.com/step-functions/) - Workflow management and task orchestration
* [Amazon S3](https://aws.amazon.com/s3/) - Object storage for any scale
* [Amazon Rekognition](https://aws.amazon.com/rekognition/) - Intelligent image and video analysis
* [AWS Lambda](https://aws.amazon.com/lambda/) - Run code without thinking about servers
* [Amazon SNS](https://aws.amazon.com/sns/) - Pub/Sub messaging
* [CloudFormation](https://aws.amazon.com/cloudformation/) - Model and set up your Amazon Web Services resources


