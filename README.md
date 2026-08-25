# AWS-LOAD-BALANCER
AWS LOAD BALANCER

REG NUMBER: 212224110043

NAME: PAVITRA J

# AIM

To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

# ALGORITHM

Step 1: Create an AMI for Auto Scaling

Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

Step 2: Create a Target Group and Load Balancer

Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

Step 3: Create a Launch Template and Auto Scaling Group

Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

Step 4: Verify Load Balancing

Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

Step 5: Test Auto Scaling

Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

Step 6: Terminate the Original Web Server

Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.
<img width="1688" height="786" alt="image" src="https://github.com/user-attachments/assets/97c55722-2511-45d2-847f-421662082b4f" />

<img width="1668" height="789" alt="image" src="https://github.com/user-attachments/assets/6c88bc7c-e3bd-4919-a5c3-5cb5133e22da" />

<img width="1438" height="672" alt="image" src="https://github.com/user-attachments/assets/da5d64e9-18d1-4e71-9d99-cf5f79c4b69f" />

<img width="1668" height="783" alt="image" src="https://github.com/user-attachments/assets/8ad91cf2-f836-4bc4-9aac-aed9acec2b94" />

<img width="1692" height="766" alt="image" src="https://github.com/user-attachments/assets/d64cc781-02a4-4148-ae53-a7cccbdbb652" />

<img width="1689" height="767" alt="image" src="https://github.com/user-attachments/assets/ecd48d0c-37b9-48a8-af19-9c954b1292b9" />

<img width="1700" height="788" alt="image" src="https://github.com/user-attachments/assets/cbf159a8-c3e6-4b52-9820-aa84e24af65e" />

# RESULT

Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
