DevOps With Fargate
================================================================


In this tutorial, we will use [AWS Cloud9](https://aws.amazon.com/tw/cloud9/) to create and co-work environment, [AWS CodePipeline](https://aws.amazon.com/tw/codepipeline/) to create an automated deployment and integration pipeline, and finally deploy on [AWS ECS – Fargate](https://aws.amazon.com/tw/fargate/) type.

![1.png](/ECS-101-DevOps_with_Fargate/images/1.png)


## Prerequisites
1. Sign-in a AWS account, and make sure you have select N.Virginia region.





## Lab tutorial
### Create a repository with AWS CodeCommit
1.1. 	Open AWS Manage Console and Sign in.

1.2. 	On the Service Menu, choose **CodeCommit** service under Developer Tools.

1.3. 	If you are first time use this service, click **Get started**, if not, click **Create Repository**.

1.4. 	Enter **workshop-commit** as the **Repository name**.

1.5. 	Click **Create Repository**.

1.6. 	Click **Skip**.

1.7. 	Notice the clone command under **Steps to clone your repository**.

1.8. 	Click **Close**.

![2.png](/ECS-101-DevOps_with_Fargate/images/2.png)


### Create a cloud-based IDE with AWS Cloud9.

2.1. 	On the Service Menu, choose **Cloud9** service under Developer Tools.

2.2. 	Click **Create environment**.

2.3. 	Type **workshop-cloud9** as the **Name**.

2.4. 	Click **Next step**.

2.5. 	Let all configure option default, click **Next step**.

2.6. 	Click **Create environment**.

2.7. 	Now you will see the Cloud9 IDE is open, wait until it done.


### Integrate Cloud9 With CodeCommit and Push First Code

3.1. 	At the bottom of page, you will see the console tab.

![3.png](/ECS-101-DevOps_with_Fargate/images/3.png)

3.2. 	Copy the follow command and paste to console.

	$ git config --global credential.helper '!aws codecommit credential-helper $@'
	$ git config --global credential.UseHttpPath true
	$ git clone https://github.com/ecloudvalley/Continuous-Integration-and-Continuous-Delivery-with-Fargate.git
	$ . Continuous-Integration-and-Continuous-Delivery-with-Fargate/ECS-101-DevOps_with_Fargate/RunFirst.sh

3.3. 	If you run successful, you will see a folder name **workshop-codecommit** at left navigation panel.

![4.png](/ECS-101-DevOps_with_Fargate/images/4.png)

3.4. 	Go to **AWS CodeCommit** page, and you will see source code are already push by bash script.


### Create a ECR Repository

4.1.    Back to ECS service page.

4.2. 	Click **Repositories** under Amazon ECR at left panel.

4.3. 	If you are first created, click **Get started**, else, click **Create repository**.

4.4. 	Type **workshop-ecr** as the Repository name.

4.5. 	Click **Next step**.

4.6. 	Click **Done**.

4.7. 	Note the **Repository URI** and copy it.

![11.png](/ECS-101-DevOps_with_Fargate/images/11.png)

4.8. 	Go back to Cloud9 IDE, open **buildspec.yml** under **build** floder and replace the Repository URI.

![12.png](/ECS-101-DevOps_with_Fargate/images/12.png)

4.9. 	Go back to Cloud9 IDE, open **buildspec.yml** under **build** floder, and replace the Container name to **workshop-container**.

![13.png](/ECS-101-DevOps_with_Fargate/images/13.png)

4.10. 	Save the file.

4.11. 	Use **Git command** push code to CodeCommit.
		
	$ git add .
	$ git commit -m "First commit"
	$ git push


### Create a Pipeline Use AWS CodePipeline

5.1. 	In the **AWS Management Console**, on the **service** menu, click **CodePipeline**.

5.2. 	Click **Get started**.

5.3. 	Type **workshoppipeline** as the pipeline name.

5.4. 	Click **Next step**.

5.5. 	Select **AWS CodeCommit** as Source provider.

5.6. 	Select **workshop-commit** as Repository name.

5.7. 	Select **master** as Branch name.

5.8. 	Click **Next step**.

5.9. 	Select **AWS CodeBuild** as Build provider.

5.10. 	Choose **Create a new build project**.

5.11. 	Type **imagebuild** as Project name.

5.12. 	Select **Ubuntu** at Operating system, select **Docker**, and select **aws/codebuild/docker:17.09.0**.

![20.png](/ECS-101-DevOps_with_Fargate/images/20.png)

5.13. 	Click **Save build project**.

5.14. 	Click **Next step**.

5.15. 	Select **Amazon ECS** as Deployment provider.

5.16. 	Select **workshop-ecs** as Cluster name.

5.17. 	Select **workshop-service** as Service name.

5.18. 	Type **images.json** as Image filename.

5.19. 	Click **Next step**.

5.20. 	At AWS Service Role, Click **Create role**.

5.21. 	Click **Allow**.

5.22. Choose **AWS-CodePipeline-Service** as Role name.

5.23. 	Click **Next step**.

5.24. 	Click **Create pipeline**.

### Config the CodeBuild buildspec.yml path

6.1.  In AWS Manage Console, click service, click **CodeBuild**.

6.2.  Select **imagebuild**, click **Actions**

6.3.  Click **Update**.

6.4.  Under **Environment: How to build**, click **Update build specification**.

6.5.  Type **build/buildspec.yml** as Buildspec name.

6.6.  Click **Update**.

### Edit the CodeBuild IAM

7.1. 	After you created pipeline, it will start running, but fail in build stage. You need to add some policies to access ECS resources.

7.2. 	In the **AWS Management Console**, on the service menu, click **IAM**.

7.3. 	Click **Role** at the left panel.

7.4. 	Find **code-build-imagebuild-service-role** and click it.

7.5. 	Click **Attach policy**.

7.6. 	Type **AmazonEC2ContainerRegistryPowerUser** in filter.

7.7. 	Select it, and click **Attach policy**.

![21.png](/ECS-101-DevOps_with_Fargate/images/21.png)

7.8. 	Back to AWS Codepipeline page, click **Retry** and **Conitune**.

7.9 	When all Stage of pipeline Success deploy, go to next step, it will need a few minutes.


### Try to See First Deploy and Test First Change

8.1. 	In AWS Manage Console, click service, and click **EC2**.

8.2. 	Click **Load Balancers** at left panel.

8.3. 	Click **workshop-ALB**, and find the DNS name.

![22.png](/ECS-101-DevOps_with_Fargate/images/22.png)

8.4. 	Open a new web page and paste it in URL line, and press enter, you will see the web which you build by Cloud9 IDE.

![23.png](/ECS-101-DevOps_with_Fargate/images/23.png)

8.5. 	Now Back to Cloud9 IDE, try to change app.py.

8.6. 	In app.py, change the version to **Second Fargate Version**.

![24.png](/ECS-101-DevOps_with_Fargate/images/24.png)

8.7. 	Save it and use **Git command** to push it to CodeCommit.

	$ git add .
	$ git commit -m "First commit"
	$ git push

8.8. 	When it push to CodeCommit successfully, it would trigger Codepipeline to automate integration and delivery, go back to CodePipeline page to see.

8.9. 	When all stage success, reload the web page, and you can see the new version is deployed.

![25.png](/ECS-101-DevOps_with_Fargate/images/25.png)

![26.png](/ECS-101-DevOps_with_Fargate/images/26.png)


### Try to Add Test Stage and Config CodeBuild

9.1. 	Go back to CodePipeline page, and click **Edit**.

9.2. 	Click **+ Stage** between Source and Build.

![28.png](/ECS-101-DevOps_with_Fargate/images/28.png)

9.3. 	Type **Test** as Stage name.

9.4. 	Click **+ Action**.

9.5. 	Select **Test** as Action category.

9.6. 	Type **CodeTest** as Action Name.

9.7. 	Select **AWS CodeBuild** as Test provider.

9.8. 	Click **Create a new build project**.

9.9. 	Type **codetest** as Project name.

9.10. 	Select Ubuntu as Operating system, select **Python**, select **aws/codebuild/python:2.7.12**. 

9.11. 	Click **Save build project**.

9.12. 	In the **Input artifacts #1**, select MyApp.

9.13. 	Click **Add action**.

9.14. 	Click **Save pipeline changes**.

9.15. 	Click **Save and continue**.

9.16. 	In AWS Manage Console, click service, click **CodeBuild**.

9.17. 	Select **codetest**, click **Actions**, click **Update**.

![29.png](/ECS-101-DevOps_with_Fargate/images/29.png)

9.18. 	Under **Environment: How to build**, click **Update build specification**.

![30.png](/ECS-101-DevOps_with_Fargate/images/30.png)

9.19. 	Type **test/buildspec.yml** as Buildspec name.

9.20. 	Click **Update**.

9.21. 	Click **Back**.

9.22. 	Back to Cloud9 IDE, change the version to **Third Fargate Version**, and use Git command to push to CodeCommit.

9.23. 	Wait all stage success, you can reload the web page to see new version.

>For this Test stage, it will run the code first before to build docker image, if code correct, it will continue run the pipeline, if code have the bug, the pipeline will stop at Test stage, this method can avoid build the bug docker images.


### Appendix. Try Some Wrong Code

10.1. 	In AWS Cloud9 IDE, try to make some bug in **app.py**.

10.2. 	Use Git command to push code and see the pipeline workflow.

10.3. 	In the AWS Manage Console, click service, and click **Codebuild**.

10.4. 	Click **codetest**.

10.5. 	Click the latest build history.

10.6. 	At the Build logs, you can see the test process, and realize how it was fail.

![31.png](/ECS-101-DevOps_with_Fargate/images/31.png)

10.7. 	You can also see the reason why this stage would fail in codepipeline by click **Details**.

![32.png](/ECS-101-DevOps_with_Fargate/images/32.png)




## Conclusion

Congratulations! You now have learned how to:

* Code by using **AWS Cloud9**.
* Integrate **AWS Cloud9** with **AWS CodeCommit**.
* Use **AWS Codepipeline**, **AWS CodeBuild**, and **Amazon ECS** to implement an automatic CI/CD workflow with Container.



