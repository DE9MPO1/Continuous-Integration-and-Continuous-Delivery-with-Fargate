Continuous Integration and Continuous Delivery With Fargate
================================================================


## About this lab
Delivering new iterations of software at a high velocity is a competitive advantage in today’s business environment. The speed at which organizations can deliver innovation to customer and adapt changing markets is a standard to determined organizations will success or failure. That’s why continuous integration and continuous delivery are important.

Nowadays, many software can help you to make a DevOps flow. But you need to waste many times to maintain those infrastructures, and sometimes will occur some human errors. It not only increase cost, but also decrease your development times.AWS provide a set of flexible DevOps tool. It can easily to integrate with another AWS service and also third party DevOps software. With those tool, you can quickly and easily to implement an automated deployment and integration pipeline for applications. All those tools are fully management.

In this tutorial, we will use [AWS Cloud9](https://aws.amazon.com/tw/cloud9/) to create and co-work environment, [AWS codepipeline](https://aws.amazon.com/tw/codepipeline/) to create an automated deployment and integration pipeline, and finally deploy on [AWS ECS – Fargate](https://aws.amazon.com/tw/fargate/) type.

![1.png](/images/1.png)


## Prerequisites
1. Sign-in a AWS account, and make sure you have select N.Virginia region.





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

	$ git config --global credential.helper '!aws codecommit credential-helper $@'
	$ git config --global credential.UseHttpPath true
	$ git clone https://github.com/ecloudvalley/Continuous-Integration-and-Continuous-Delivery-with-Fargate.git
	$ . Continuous-Integration-and-Continuous-Delivery-with-Fargate/RunFirst.sh

1.19. 	If you run successful, you will see a folder name **workshop-codecommit** at left navigation panel.

![4.png](/images/4.png)

1.20. 	Go to **AWS CodeCommit** page, and you will see source code are already push by bash script.


#### Create a Cluster, Task Definition, and Service Using Fargate

1.21. 	On the Service Menu, choose **Elastic Container Service** under Compute.

1.22. 	Click **Get started**.

1.23. 	Click **Cancel**.

1.24. 	If you see this page, it means that you can do next.

![9.png](/images/9.png)

1.25. 	Click **Create Clusters**.

1.26. 	Select **Networking only**, and click **Next step**.

1.27. 	Type **workshop-ecs** as the Cluster name.

1.28. 	Click **Create VPC**.

1.29. 	Create your own CIDR which not affect others VPC.

1.30. 	Click **Create**.

1.31. 	When it created successfully, click **View Clusters**.

1.32. 	If you see the cluster’s status is **ACTIVE**, you can do next step.

![10.png](/images/10.png)

1.33. 	Click **Repositories** under Amazon ECR at left panel.

1.34. 	If you are first created, click **Get started**, else, click **Create repository**.

1.35. 	Type **workshop-ecr** as the Repository name.

1.36. 	Click **Next step**.

1.37. 	Click **Done**.

1.38. 	Note the **Repository** URI and copy it.

![11.png](/images/11.png)

1.39. 	Go back to Cloud9 IDE to replace the Repository URI.

![12.png](/images/12.png)

1.40. 	Use **Git command** push code to CodeCommit.

1.41. 	Back to ECS page, click **Task Definitions** at left panel.

1.42. 	Click **Create new Task Definition**.

1.43. 	Select **Fargate**, and click **Next step**.

1.44. 	Type **workshop-task** as the Task Definition Name.

1.45. 	Select **None** as Task Role

1.46. 	Under the Task Size, select **0.5GB** as Task memory, **0.25vCPU** as Task CPU.

1.47. 	Click **Add container**.

1.48. 	Type **workshop-container** as Container name.

1.49. 	Paste the **Repository URI** you noted previously into Image field.

1.50. 	At the Port mappings part, Type **80** as Container port.

1.51. 	Click **Add**.

1.52. 	Click **Create**.

1.53. 	Go back to Cloud9 IDE to replace the Container name.

![13.png](/images/13.png)

1.54. 	Use **Git command** push code to CodeCommit.

1.55. 	Back to ECS page, click **Action**, and Select **Create Service**.

![14.png](/images/14.png)

1.56. 	Choose **Fargate** as Launch type.

1.57. 	Type **workshop-service** as the Service name.

1.58. 	In Number of tasks, enter **1**.

1.59. 	Click **Next step**.

![15.png](/images/15.png)

1.60. 	Select VPC which you create previously.

1.61. 	At Subnets, select all two subnets.

1.62. 	Under Load balancing, choose **Application Load Balancer**.

1.63. 	You will see a warning which mean you need to create ALB, click **EC2 Console**.

![16.png](/images/16.png)

1.64. 	Select **Create** under Application Load Balancer.

1.65. 	Type **workshop-ALB** as Name.

1.66. 	Under Availability Zones, choose the VPC you created previously, and select both.

![17.png](/images/17.png)

1.67. 	Click **Next: Configure Security Settings**.

1.68. 	Click **Next: Configure Security Groups**.

1.69. 	Select **Create a new security group**.

1.70. 	Type **workshop-ALB-SG** as Security group name.

1.71. 	At Type part, Select **HTTP**.

1.72. 	At Source part, Select **Anywhere**.

1.73. 	Click **Next: Configure Routing**.

1.74. 	Type **workshop-TG** as the name.

1.75. 	At the Target type, select **ip**.

1.76. 	Click **Next: Register Target**.

1.77. 	Click **Next: Review**.

1.78. 	Click **Create**.

1.79. 	When it created successfully, click **Close**.

1.80. 	Back to ECS create service page.

1.81. 	Click **Reload**.

![18.png](/images/18.png)

1.82. 	Select **workshop-ALB** as Load balancer name.

1.83. 	Under Container to load balance, click **Add to load balancer**.

1.84. 	At the Target group name, select **workshop-TG**.

![19.png](/images/19.png)

1.85. 	Click **Next step**.

1.86. 	Let option default, click **Next step**.

1.87. 	Click **Create Service**.

1.88. 	When it created Successfully, click **View Service**, and you can do next step.


#### Create a Pipeline Use AWS CodePipeline

1.89. 	In the **AWS Management Console**, on the **service** menu, click **CodePipeline**.

1.90. 	Click **Get started**.

1.91. 	Type **workshoppipeline** as the pipeline name.

1.92. 	Click **Next step**.

1.93. 	Select **AWS CodeCommit** as Source provider.

1.94. 	Select **workshop-commit** as Repository name.

1.95. 	Select **master** as Branch name.

1.96. 	Click **Next step**.

1.97. 	Select **AWS CodeBuild** as Build provider.

1.98. 	Choose **Create a new build project**.

1.99. 	Type **imagebuild** as Project name.

1.100. 	Select Ubuntu at Operating system, select **Docker**, and select **aws/codebuild/docker:17.09.0**.

![20.png](/images/20.png)

1.101. 	Click **Save build project**.

1.102. 	Click **Next step**.

1.103. 	Select **Amazon ECS** as Deployment provider.

1.104. 	Select **workshop-ecs** as Cluster name.

1.105. 	Select **workshop-service** as Service name.

1.106. 	Type **images.json** as Image filename.

1.107. 	Click **Next step**.

1.108. 	At AWS Service Role, Click **Create role**.

1.109. 	Click **Allow**.

1.110. 	Click **Next step**.

1.111. 	Click **Create pipeline**.

#### Config the CodeBuild buildspec.yml path

1.112.  In AWS Manage Console, click service, click **CodeBuild**.

1.113.  Select **imagebuild**, click **Actions**

1.114.  Click **Update**.

1.115.  Under **Environment: How to build**, click **Update build specification**.

1.116.  Type **build/buildspec.yml** as Buildspec name.

1.117.  Click **Update**.

#### Edit the CodeBuild IAM

1.118. 	After you created pipeline, it will start running, but fail in build stage. You need to add some policies to access ECS resources.

1.119. 	In the **AWS Management Console**, on the service menu, click **IAM**.

1.120. 	Click **Role** at the left panel.

1.121. 	Find **code-build-imagebuild-service-role** and click it.

1.122. 	Click **Attach policy**.

1.123. 	Type **AmazonEC2ContainerRegistryPowerUser** in filter.

1.124. 	Select it, and click **Attach policy**.

![21.png](/images/21.png)

1.125. 	Back to AWS Codepipeline page, click **Retry**.


#### Try to See First Deploy and Test First Change

1.126. 	When all Stage Success, In AWS Manage Console, click service, and click **EC2**.

1.127. 	Click **Load Balancers** at left panel.

1.128. 	Click **workshop-ALB**, and find the DNS name.

![22.png](/images/22.png)

1.129. 	Open a new web page and paste it in URL line, and press enter, you will see the web which you build by Cloud9 IDE.

![23.png](/images/23.png)

1.130. 	Now Back to Cloud9 IDE, try to change app.py.

1.131. 	In app.py, change the version to **Second Fargate Version**.

![24.png](/images/24.png)

1.132. 	Save it and use **Git command** to push it to CodeCommit.

1.133. 	When it push to CodeCommit successfully, it would trigger Codepipeline to automate integration and delivery, go back to CodePipeline page to see.

1.134. 	When all stage success, reload the web page, and you can see the new version is deployed.

![25.png](/images/25.png)

![26.png](/images/26.png)


#### Try to Add Test Stage and Config CodeBuild

1.135. 	Go back to CodePipeline page, and click **Edit**.

1.136. 	Click **+ Stage** between Source and Build.

![28.png](/images/28.png)

1.137. 	Type **Test** as Stage name.

1.138. 	Click **+ Action**.

1.139. 	Select **Test** as Action category.

1.140. 	Type **CodeTest** as Action Name.

1.141. 	Select **AWS CodeBuild** as Test provider.

1.142. 	Click **Create a new build project**.

1.143. 	Type **codetest** as Project name.

1.144. 	Select Ubuntu as Operating system, select **Python**, select **aws/codebuild/python:2.7.12**. 

1.145. 	Click **Save build project**.

1.146. 	In the **Input artifacts #1**, select MyApp.

1.147. 	Click **Add action**.

1.148. 	Click **Save pipeline changes**.

1.149. 	Click **Save and continue**.

1.150. 	In AWS Manage Console, click service, click **CodeBuild**.

1.151. 	Select **codetest**, click **Actions**, click **Update**.

![29.png](/images/29.png)

1.152. 	Under **Environment: How to build**, click **Update build specification**.

![30.png](/images/30.png)

1.153. 	Type **test/buildspec.yml** as Buildspec name.

1.154. 	Click **Update**.

1.155. 	Click **Back**.

1.160. 	Back to Cloud9 IDE, change the version to **Third Fargate Version**, and use Git command to push to CodeCommit.

1.161. 	Wait all stage success, you can reload the web page to see new version.
* For this Test stage, it will run the code first before to build docker image, if code correct, it will continue run the pipeline, if code have the bug, the pipeline will stop at Test stage, this method can avoid build the bug docker images.


#### Try Some Wrong Code

1.162. 	In AWS Cloud9 IDE, try to make some bug in **app.py**.

1.163. 	Use Git command to push code and see the pipeline workflow.

1.164. 	In the AWS Manage Console, click service, and click **Codebuild**.

1.165. 	Click **codetest**.

1.166. 	Click the latest build history.

1.167. 	At the Build logs, you can see the test process, and realize how it was fail.

![31.png](/images/31.png)

1.168. 	You can also see the reason why this stage would fail in codepipeline by click **Details**.

![32.png](/images/32.png)




## Conclusion

Congratulations! You now have learned how to:

* Code by using **AWS Cloud9**.
* Integrate **AWS Cloud9** with **AWS CodeCommit**.
* Create **Amazon ECS** using **Fargate** type.
* Use **AWS Codepipeline**, **AWS CodeBuild**, and **Amazon ECS** to implement an automatic CI/CD workflow with Container.



