Continuous Integration and Continuous Delivery with AWS Fargate (Amazon ECS)
================================================================

## Why need DevOps Tool
Delivering new iterations of software at a high velocity is a competitive advantage in today’s business environment. The speed at which organizations can deliver innovation to customer and adapt changing markets is a standard to determined organizations will success or failure. That’s why continuous integration and continuous delivery are important.

Nowadays, many software can help you to make a DevOps flow. But you need to waste many times to maintain those infrastructures, and sometimes will occur some human errors. It not only increase cost, but also decrease your development times. AWS provide a set of flexible DevOps tool. It can easily to integrate with another AWS service and also third party DevOps software. With those tool, you can quickly and easily to implement an automated deployment and integration pipeline for applications. All those tools are fully management.

## Scenario
In this tutorial, we will using [AWS Fargate](https://aws.amazon.com/fargate/) to run containers without having to manage servers or clusters, Fargate lets you focus on designing and building your applications instead of managing the infrastructure that runs them. With Fargate launch type is one mode of [Amazon ECS](https://aws.amazon.com/ecs/), all you have to do is package your application in containers, specify the CPU and memory requirements, define networking and IAM policies, and launch the application. Amazon ECS keeps track of all the CPU, memory and other resources in your cluster, and also finds the best server for a container to run on based on your specified resource requirements.

After create Amazon ECS using Fargate type, we will code by using [AWS Cloud9](https://aws.amazon.com/cloud9/) which is a cloud-based integrated development environment (IDE) that lets you write, run, and debug your code with just a browser. Integrate AWS Cloud9 with [AWS CodeCommit](https://aws.amazon.com/codecommit/), use [AWS Codepipeline](https://aws.amazon.com/codepipeline/), [AWS CodeBuild](https://aws.amazon.com/codebuild/), and Amazon ECS to implement an automatic CI/CD workflow with Container.

First step: [Create a Cluster, Task Definition, and Service Using Fargate](https://github.com/ecloudvalley/Continuous-Integration-and-Continuous-Delivery-with-Fargate/tree/master/ECS-100-Service_with_Fargate)
Second
