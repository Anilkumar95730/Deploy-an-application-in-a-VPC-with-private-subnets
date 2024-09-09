# Deploy-an-application-in-a-VPC-with-private-subnets
![image](https://github.com/user-attachments/assets/b1433edc-b800-4f11-b317-af0ad4d73445)
The VPC has public subnets and private subnets in each of the two Availability Zones. Each public subnet contains a NAT gateway and a load balancer node. The servers run in the private subnets, are launched and terminated by using an Auto Scaling group and receive traffic from the load balancer. The servers can connect to the internet by using the NAT gateway.

Log in to your AWS Management Console using your credentials. Navigate to VPC Dashboard by searching for “VPC” in the AWS services search bar or directly accessing it from the services menu.

# Create a VPC:
Go to the VPC dashboard in the AWS Management Console. Click on “Create VPC”. Provide a name for your VPC, select the CIDR block, and enable DNS support. Create two public subnets and two private subnets, each in a different availability zone of the Mumbai region (1a and 1b). I have selected Mumbai region. You can select anything as you need. Make sure to associate a route table with each subnet and configure the public subnets to have access to the internet through an Internet Gateway (IGW)
![image](https://github.com/user-attachments/assets/d3bb256d-6d87-4669-8624-ead5636df3ae)
# Creation of an Auto Scaling Group:
Go to the EC2 dashboard and navigate to the “Auto Scaling Groups” section. Click on “Create Auto Scaling Group”. Choose the launch template option and create a launch template with the desired configuration (minimum 1 instance, maximum 4 instances, desired capacity 2 instances). Launch Templates allow you to create a saved instance configuration that can be reused, shared and launched at a later time. Templates can have multiple versions. Specify the AMI, instance type, security groups (allowing necessary traffic), key pair, etc. Configure scaling policies if needed. Associate the auto scaling group with the private subnets in the Network tab as shown in the image below.
![image](https://github.com/user-attachments/assets/308524d0-f61a-44f3-8bb6-23a81c58b730)
# Creation of a Bastion Host:
Launch a new EC2 instance in one of the public subnets (public subnet in Mumbai 1a or 1b). Ensure that the security group allows SSH access from your IP address. Assign an Elastic IP to the instance for persistent public IP. Connect to the bastion host using SSH.
![image](https://github.com/user-attachments/assets/9c54eb14-aed2-484a-8c5c-959b9a9072fd)
# Deployment of Sample Application on Primary Web Server:
Copy the PEM file to the bastion host which is needed to connect to EC2 instances that are in the private subnet. SSH into the primary web server (one of the instances in the private subnet). Deploy your sample application and run a Python HTTP server. Test the application locally on the primary web server to ensure it’s running correctly.

# Creation of Load Balancer and Target Group:
Go to the EC2 dashboard and navigate to the “Load Balancers” section. Click on “Create Load Balancer” and choose the type (e.g., Application Load Balancer). Configure listeners and select the availability zones. Create a target group and add the primary and secondary web servers as targets. Configure health checks and routing settings as needed.
![image](https://github.com/user-attachments/assets/c4289da3-006d-426c-8f8d-b1add5e0e006)
and Target group
![image](https://github.com/user-attachments/assets/ef3cd7f7-f2f3-49c8-943d-3ac51064db0f)
# Ec2 instances connect pdf as a link :
    (https://drive.google.com/file/d/15Omr_W8kcFVJnPQuc1HkvKZwhjz75aiN/view?usp=drivesdk)
result link :
http://project1-432817283.us-east-1.elb.amazonaws.com/

Result Images
