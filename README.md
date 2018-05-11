Continuous Integration and Continuous Delivery With Fargate
================================================================


## About this lab
Delivering new iterations of software at a high velocity is a competitive advantage in today’s business environment. The speed at which organizations can deliver innovation to customer and adapt changing markets is a standard to determined organizations will success or failure. That’s why continuous integration and continuous delivery are important.

Nowadays, many software can help you to make a DevOps flow. But you need to waste many times to maintain those infrastructures, and sometimes will occur some human errors. It not only increase cost, but also decrease your development times.AWS provide a set of flexible DevOps tool. It can easily to integrate with another AWS service and also third party DevOps software. With those tool, you can quickly and easily to implement an automated deployment and integration pipeline for applications. All those tools are fully management.

In this tutorial, we will use [AWS Cloud9](https://aws.amazon.com/tw/cloud9/) to create and co-work environment, [AWS codepipeline](https://aws.amazon.com/tw/codepipeline/) to create an automated deployment and integration pipeline, and finally deploy on [AWS ECS – Fargate](https://aws.amazon.com/tw/fargate/) type.

![1.png](/images/1.png)


## Prerequisites
1. Sign-in a AWS account, and make sure you have select N.Virginia region.

2. Download the source file from github.



## Lab tutorial
#### Create a repository with AWS CodeCommit
1.1. 	Open AWS Manage Console and Sign in.

1.2. 	On the Service Menu, choose **CodeCommit** service under Developer Tools.

1.3. 	If you are first time use this service, click **Get started**, if not, click **Create Repository**.

1.4. 	Enter **workshop-commit** as the **Repository name**.

1.5. 	Click **Create Repository**.

1.6. 	Click **Skip**.

1.7. 	Notice the clone command under **Steps to clone your repository**.

1.8. 	Click **Close**.

![2.png](/images/2.png)


#### Create a cloud-based IDE with AWS Cloud9.

1.9. 	On the Service Menu, choose **Cloud9** service under Developer Tools.

1.10. 	Click **Create environment**.

1.11. 	Type **workshop-cloud9** as the **Name**.

1.12. 	Click **Next step**.

1.13. 	Let all configure option default, click **Next step**.

1.14. 	Click **Create environment**.

1.15. 	Now you will see the Cloud9 IDE is open, wait until it done.


#### Integrate Cloud9 With CodeCommit and Push First Code

1.16. 	At the bottom of page, you will see the console tab.

![3.png](/images/3.png)

1.17. 	Copy the follow command and paste to console.

	git config --global credential.helper '!aws codecommit credential-helper $@'
	git config --global credential.UseHttpPath true

1.18. 	Paste the command that you notice at **step 1.8**.

1.19. 	If you clone successful, you will see a folder name **workshop-codecommit** at left navigation panel.

![4.png](/images/4.png)

1.20. 	At the **workshop-commit** folder layer create a **New File**, and named **app.py**.

1.21. 	Copy code in **app.py** which you download into **Cloud9’s app.py**.

![5.png](/images/5.png)

1.22. 	Create a **New File**, and named **requirements.txt**.

1.23. 	Copy code in **requirements.txt** which you download into **Cloud9’s requirements.txt**.

![6.png](/images/6.png)

1.24. 	Create a **New File**, and named **Dockerfile**.

1.25. 	Copy code in **Dockerfile** which you download into **Cloud9’s Dockerfile**.

![7.png](/images/7.png)

1.26. 	Create a **New File**, and named **buildspec.yml**.

1.27. 	Copy code in **build/buildspec.yml** which you download into **Cloud9’s buildspec.yml**.

![8.png](/images/8.png)

1.28. 	Select **File** in Tool bar, and click **Save all**.

1.29. 	In console, enter the follow code to push your code to CodeCommit.

	cd workshop-commit
	git add .
	git commit -m "First Commit "
	git push

1.30. 	Go to **AWS CodeCommit** page, and you will see those code you push previously.


#### Create a Cluster, Task Definition, and Service Using Fargate

1.31. 	On the Service Menu, choose **Elastic Container Service** under Compute.

1.32. 	Click **Get started**.

1.33. 	Click **Cancel**.

1.34. 	If you see this page, it means that you can do next.

![9.png](/images/9.png)

1.35. 	Click **Create Clusters**.

1.36. 	Select **Networking only**, and click **Next step**.

1.37. 	Type workshop-ecs as the Cluster name.

1.38. 	Click Create VPC.

1.39. 	Create your own CIDR which not affect others VPC.

1.40. 	Click Create.

1.41. 	When it created successfully, click View Clusters.

1.42. 	If you see the cluster’s status is ACTIVE, you can do next step.




#### Exam your Resource

1.66. 	In the *AWS Management Console*, on the *service* menu, click *EC2*.

1.67. 	Click Instance, select *ECS Instance-EC2ContainerService-default* instance.

1.68. 	On the *Description* tab in the lower pane, copy the *IPv4 Public IP* to your clipboard.

1.69. 	Open a new browser tab, paste the IP address from your clipboard and hit Enter. The Container should appear.

1.70. 	In the browser, you will see:
*Hello World!*




## Conclusion

Congratulations! You now have learned how to:

* Setup a Docker engine.
* Create a container repository.
* Tag and push image to Amazon ECR.


