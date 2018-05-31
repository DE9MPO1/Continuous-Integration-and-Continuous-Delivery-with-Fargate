Service With Fargate
================================================================

## Lab tutorial
#### Create a Cluster, Task Definition, and Service Using Fargate

1.1. 	On the Service Menu, choose **Elastic Container Service** under Compute.

1.2. 	Click **Get started**.

1.3. 	Click **Cancel**.

1.4. 	If you see this page, it means that you can do next.

![9.png](/ECS-100-Service_with_Fargate/images/9.png)

1.5. 	Click **Create Clusters**.

1.6. 	Select **Networking only**, and click **Next step**.

1.7. 	Type **workshop-ecs** as the Cluster name.

1.8. 	Click **Create VPC**.

1.9. 	Create your own CIDR which not affect others VPC.

1.10. 	Click **Create**.

1.11. 	When it created successfully, click **View Clusters**.

1.12. 	If you see the cluster’s status is **ACTIVE**, you can do next step.

![10.png](/ECS-100-Service_with_Fargate/images/10.png)

1.13. 	Back to ECS page, click **Task Definitions** at left panel.

1.14. 	Click **Create new Task Definition**.

1.15. 	Select **Fargate**, and click **Next step**.

1.16. 	Type **workshop-task** as the Task Definition Name.

1.17. 	Select **None** as Task Role

1.18. 	Under the Task Size, select **0.5GB** as Task memory, **0.25vCPU** as Task CPU.

1.19. 	Click **Add container**.

1.20. 	Type **workshop-container** as Container name.

1.21. 	Paste the **httpd** into Image field.

1.22. 	At the Port mappings part, Type **80** as Container port.

1.23. 	Click **Add**.

1.24. 	Click **Create**.

1.25. 	Back to ECS page, click **Action**, and Select **Create Service**.

![14.png](/ECS-100-Service_with_Fargate/images/14.png)

1.26. 	Choose **Fargate** as Launch type.

1.27. 	Type **workshop-service** as the Service name.

1.28. 	In Number of tasks, enter **1**.

1.29. 	Click **Next step**.

![15.png](/ECS-100-Service_with_Fargate/images/15.png)

1.30. 	Select VPC which you create previously.

1.31. 	At Subnets, select all two subnets.

1.32. 	Under Load balancing, choose **Application Load Balancer**.

1.33. 	You will see a warning which mean you need to create ALB, click **EC2 Console**.

![16.png](/ECS-100-Service_with_Fargate/images/16.png)

1.34. 	Select **Create** under Application Load Balancer.

1.35. 	Type **workshop-ALB** as Name.

1.36. 	Under Availability Zones, choose the VPC you created previously, and select both.

![17.png](/ECS-100-Service_with_Fargate/images/17.png)

1.37. 	Click **Next: Configure Security Settings**.

1.38. 	Click **Next: Configure Security Groups**.

1.39. 	Select **Create a new security group**.

1.40. 	Type **workshop-ALB-SG** as Security group name.

1.41. 	At Type part, Select **HTTP**.

1.42. 	At Source part, Select **Anywhere**.

1.43. 	Click **Next: Configure Routing**.

1.44. 	Type **workshop-TG** as the name.

1.45. 	At the Target type, select **ip**.

1.46. 	Click **Next: Register Target**.

1.47. 	Click **Next: Review**.

1.48. 	Click **Create**.

1.49. 	When it created successfully, click **Close**.

1.50. 	Back to ECS create service page.

1.51. 	Click **Reload**.

![18.png](/ECS-100-Service_with_Fargate/images/18.png)

1.52. 	Select **workshop-ALB** as Load balancer name.

1.53. 	Under Container to load balance, click **Add to load balancer**.

1.54. 	At the Target group name, select **workshop-TG**.

![19.png](/ECS-100-Service_with_Fargate/images/19.png)

1.55. 	Click **Next step**.

1.56. 	Let option default, click **Next step**.

1.57. 	Click **Create Service**.

1.58. 	When it created Successfully, click **View Service**, and you can do next step.

#### Verify the Service

2.1. Go to EC2 page, and click **Load Balancers**, then select the load balancer you created.

2.2. Copy the **DNS**, and paste to browser URL, and click **Enter**.

2.3. If the service created successfully, you will see **It works!**.




## Conclusion

Congratulations! You now have learned how to:

* Create **Amazon ECS** using **Fargate** type.




