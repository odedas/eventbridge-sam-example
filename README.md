# EventBridge Lambda-to-Lambda example

This example SAM application creates two Lambda functions, called invoiceService and orderService. It creates a rule that listens for events and routes to the target, invoiceService.

When the orderService function is invoked, it puts a event onto the EventBridge default event bus. This then invokes the invoiceService target.

Important: this application uses various AWS services and there are costs associated with these services after the Free Tier usage - please see the [AWS Pricing page](https://aws.amazon.com/pricing/) for details. You are responsible for any AWS costs incurred. No warranty is implied in this example.

```bash
.
├── README.MD                   <-- This instructions file
├── invoiceService              <-- Source code for a lambda function
│   └── app.js                  <-- Main Lambda handler
├── orderService                <-- Source code for a lambda function
│   └── app.js                  <-- Main Lambda handler
│   └── package.json            <-- NodeJS dependencies and scripts
├── template.yaml               <-- SAM template
```

## Requirements

* AWS CLI already configured with Administrator permission
* [NodeJS 12.x installed](https://nodejs.org/en/download/)

## Installation Instructions

1. [Create an AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html) if you do not already have one and login.

1. From the command line, run:
```
sam build
sam deploy --guided
```
During the guided SAM process, choose the AWS Region where you want to install this application, and allow the permissions required to complete the installation.

## How it works

When the orderFunction service is executed, it sends an event to the default event bus. This event is evaluated by a event rule created by the application. It then triggers the target Lambda function, invoiceFunction.

The purpose of this application is to show how two separate Lambda functions can interact using an event bus, without direct invocation.

==============================================

Copyright 2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.

SPDX-License-Identifier: MIT-0

## summery
===============
Amazon EventBridge is a serverless event bus service that helps connect external SaaS providers with your own applications and AWS services. EventBridge enables you to decouple your architectures to make it faster to build and innovate, using routing rules to deliver events to selected targets. For serverless builders developing event-driven applications, EventBridge makes it easy to discover event schemas, create a registry of events, and use a robust, highly available event bus to connect data across services

# resource
# Learn how to use Amazon EventBridge to build decoupled, event-driven architectures.
https://us-west-2.console.aws.amazon.com/events/home?region=us-west-2#/gettingstarted
https://www.youtube.com/watch?v=TXh5oU_yo9M&t=164s


points to remember
------------------
1. tyipical scenario is where you start from a simple decuppeled architecture and as more as it gets bigger it become hard to keep decupeling,
its hard to manage state of a workflow
its hard to add more consumers to your flow
you need to keep versioning
you need to deal with error handeling
avalability - much like synchrnus flow vs observable
so you need an orchestration that can help you with this chalanges
So the goal is to moving into event architecture:
you start your flow with an event or in a schedule manner, this goes to EventBus
in the EventBus there are rules and routing that passes request to independent parts(serverless)
parts can "talk" to each other through EventBride and not directly
price: 1$ per milion events
decupeling
simplified event routing, you can change/add rules without interfier with other that already working
third party integration
avalability and improved error handeling

# how to use (git clone https://github.com/jbesw/eventbridge-sam-example.git)
1. on the console trigger the invoce service
    aws lambda invoke --function-name arn:aws:lambda:us-west-2:334940955711:function:eventBridge-demo-invoiceServiceFunction-GT6U6W9h9JN6 output.txt
2. open CloudWath console and view logs,
3. open EventBridge console and view bus definition, rule definition
4. change rule from event to schedule
5. to view logs on console type 
    sam logs -n invoiceServiceFunction --stack-name eventBridge-demo -t
6. change target to a step-function flow
6. clean resources after demo!