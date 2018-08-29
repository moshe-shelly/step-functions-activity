# Step Functions - Long Asynchronous Activities

This sample code is an example of using Step Functions for long asynchronous tasks. For demonstration we will use a video analysis workflow - use ML to detect unsafe content with Amazon Rekognition.
The flow in high level would be:  

## Background

With Step Functions you define a work flow from series of steps, to create a state machine. *Activities* are an AWS Step Functions concept that refers to a task to be performed by a worker. This can be used to run long running processes, and notify the state machine that a task is done.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```


## Deployment

To deploy the solution in your account simply launch the provided cloud formation template.

## Built With


* [AWS](https://aws.amazon.com/) - Amazon Web Services
* [CloudFormation](https://aws.amazon.com/cloudformation/) - Model and set up your Amazon Web Services resources


## License


