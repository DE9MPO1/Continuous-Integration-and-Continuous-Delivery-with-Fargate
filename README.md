Continuous Integration and Continuous Delivery With Fargate/EC2 Container
================================================================

## Scenario
Delivering new iterations of software at a high velocity is a competitive advantage in today’s business environment. The speed at which organizations can deliver innovation to customer and adapt changing markets is a standard to determined organizations will success or failure. That’s why continuous integration and continuous delivery are important.

Nowadays, many software can help you to make a DevOps flow. But you need to waste many times to maintain those infrastructures, and sometimes will occur some human errors. It not only increase cost, but also decrease your development times. AWS provide a set of flexible DevOps tool. It can easily to integrate with another AWS service and also third party DevOps software. With those tool, you can quickly and easily to implement an automated deployment and integration pipeline for applications. All those tools are fully management.

In this tutorial, we will use [AWS Cloud9](https://aws.amazon.com/cloud9/) to create and co-work environment, AWS codepipeline to create an automated deployment and integration pipeline, and finally deploy on [AWS Fargate](https://aws.amazon.com/fargate/) and [AWS ECS – EC2 Container](https://aws.amazon.com/ecs/) type. Following are the architecture of this tutorial:

![architecture.png](/architecture.png)
