<h1>Module 6 Guided Lab - Creating a Virtual Private Cloud</h1>
<h2>Lab overview and objectives</h2>
FYI: <a href="https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html">What is Amazon VPC?</a><br><br>
Traditional networking is difficult. It involves equipment, cabling, complex configurations, and specialist skills. Amazon Virtual Private Cloud (Amazon VPC) hides the complexity, and simplifies the deployment of secure private networks.<br><br>

This lab shows you how to build your own virtual private cloud (VPC), deploy resources, and create private peering connections between VPCs.<br><br>

After completing this lab, you should be able to:<br>
<ul><li>Deploy a VPC
<li>Create an internet gateway and attach it to the VPC
<li>Create a public subnet
<li>Create private subnet
<li>Create an application server to test the VPC</li></ul>
<img src="https://i.imgur.com/DAjP5gL.png" width=60%><br>

<h2>Task 1: Creating a VPC</h2>
You will begin by using Amazon VPC to create a new virtual private cloud, or VPC.<br><br>

A VPC is a virtual network that is dedicated to your Amazon Web Services (AWS) account. It is logically isolated from other virtual networks in the AWS Cloud. You can launch AWS resources, such as Amazon Elastic Compute Cloud (Amazon EC2) instances, into the VPC. You can configure the VPC by modifying its IP address range, and create subnets. You can also configure route tables, network gateways, and security settings.<br><br>

1.In the search box to the right of  Services, search for and choose VPC to open the VPC console.<br>
The VPC console provides a wizard that can automatically create several VPC architectures. However, in this lab, you will create the VPC components manually.<br><br>

2.In the left navigation pane, choose Your VPCs.<br>
A default VPC is provided so that you can launch resources as soon as you start using AWS. There is also a Shared VPC that you will use later in the lab. However, you will now create your own Lab VPC.<br>
The VPC will have a Classless Inter-Domain Routing (CIDR) range of 10.0.0.0/16, which includes all IP address that start with 10.0.x.x. It contains over 65,000 addresses. You will later divide the addresses into separate subnets.<br><br>

3.Choose Create VPC and configure these settings:<br>
<ul><li>Name tag: Lab VPC
<li>IPv4 CIDR block: 10.0.0.0/16
<li>Choose Create VPC</li></ul>
A message that you successfully created the VPC appears.<br>
<img src="https://i.imgur.com/meF6xdz.png" width=60%>
<img src="https://i.imgur.com/CoOmBZO.png" width=60%>

4.In the lower half of the page, choose the Tags tab.<br>
Tags are useful for identifying resources.<br>
For example, you can use a tag to identify cost centers or different environments (such as development, test, or production).<br>
<img src="https://i.imgur.com/mq6qK21.png" width=60%><br>
5.Choose Actions and select Edit VPC settings.<br>
This option assigns a friendly Domain Name System (DNS) name to EC2 instances in the VPC, such as:<br>
ec2-52-42-133-255.us-west-2.compute.amazonaws.com<br>
<img src="https://i.imgur.com/vKTEUWa.png" width=60%><br>
6.Select Enable DNS hostname and then choose Save<br> 
Any EC2 instances that are launched into the VPC will now automatically receive a DNS hostname.<br>
You can also add a more meaningful DNS name (such as app.example.com) later by using Amazon Route 53.<br>
<img src="https://i.imgur.com/c50hKar.png" width=60%>

<h2>Task 2: Creating subnets</h2>
A subnet is a subrange of IP addresses in the VPC. AWS resources can be launched into a specified subnet. Use a public subnet for resources that must be connected to the internet, and use a private subnet for resources that must remain isolated from the internet.<br><br>
In this task, you will create a public subnet and a private subnet:<br>
<img src="https://i.imgur.com/aWrVzIT.png" width=60%><br>

<h3>Creating a public subnet</h3>
The public subnet will be used for internet-facing resources.<br><br>
7.In the left navigation pane, choose Subnets.<br>
<img src="https://i.imgur.com/2kCtMb6.png" width=60%>
8.Choose Create subnet and configure these settings:<br>
<ul><li>VPC ID: Lab VPC
<li>Subnet name: Public Subnet
<li>Availability Zone: Select the first Availability Zone in the list (do not keep the No Preference default)
<li>IPv4 CIDR block: 10.0.0.0/24
<li>Choose Create subnet</li></ul>
💬The VPC has a CIDR block of 10.0.0.0/16, which includes all 10.0.x.x IP addresses.<br>
The subnet you just created has a CIDR block of 10.0.0.0/24, which includes all 10.0.0.x IP addresses.<br>
They might look similar, but the subnet is smaller than the VPC because of the /24 in the CIDR range.<br><br>
You will now configure the subnet to automatically assign a public IP address for all instances that are launched in it.<br>
<img src="https://i.imgur.com/PQ4iwzi.png" width=60%>
<img src="https://i.imgur.com/jJMQ3id.png" width=60%>
9.Select  Public Subnet.<br>
<img src="https://i.imgur.com/am8OtVl.png" width=60%>
10.Choose Actions and select Edit subnet settings, then:<br>
<ul><li>Select Enable auto-assign public IPv4 address
<li>Choose Save</li></ul>
‼️Though this subnet is named Public Subnet, it is not yet public.<br>
A public subnet must have an internet gateway, which you attach in the next task.<br>
<img src="https://i.imgur.com/iuwCrwB.png" width=60%><br>

<h3>Creating a private subnet</h3>
11.The private subnet will be used for resources that must remain isolated from the internet.<br><br>
Use what you just learned to create another subnet with these settings:
<ul><li>VPC ID: Lab VPC
<li>Subnet name: Private Subnet
<li>Availability Zone: Select the first Availability Zone in the list (do not keep the No Preference default)
<li>IPv4 CIDR block: 10.0.2.0/23</li></ul>
The CIDR block of 10.0.2.0/23 includes all IP addresses that start with 10.0.2.x and 10.0.3.x. This is twice as large as the public subnet because most resources should be kept private, unless they specifically must be accessible from the internet.<br><br>
Your VPC now has two subnets. However, the public subnet is totally isolated and cannot communicate with resources outside the VPC. You will next configure the public subnet to connect to the internet via an internet gateway.
<img src="https://i.imgur.com/PQ4iwzi.png" width=60%>
<img src="https://i.imgur.com/Wp3k4yA.png" width=60%>

<h2>Task 3: Creating an internet gateway</h2>
An internet gateway is a horizontally scaled, redundant, and highly available VPC component. It allows communication between the instances in a VPC and the internet. It imposes no availability risks or bandwidth constraints on network traffic.<br><br>

An internet gateway serves two purposes:<br>
<ul><li>To provide a target in route tables that connects to the internet
<li>To perform network address translation (NAT) for instances that were assigned public IPv4 addresses</li></ul>
In this task, you will create an internet gateway so that internet traffic can access the public subnet.<br><br>

12.In the left navigation pane, choose Internet Gateways.<br>
<img src="https://i.imgur.com/OPW3fV2.png" width=60%><br>
13.Choose Create internet gateway and configure these settings:<br>
<ul><li>Name tag: Lab IGW
<li>Choose Create internet gateway</li></ul>
You can now attach the internet gateway to your Lab VPC.<br>
<img src="https://i.imgur.com/QG6bhOK.png" width=60%><br>
14.Choose Actions then Attach to VPC, and configure these settings:<br>
<ul><li>Available VPCs: Place you cursor in the search box, then select Lab VPC 
<li>Choose Attach internet gateway</li></ul>
This action will attach the internet gateway to your Lab VPC. Though you created an internet gateway and attached it to your VPC, you must also configure the public subnet route table so it uses the internet gateway.
<img src="https://i.imgur.com/HSMRj4Y.png" width=60%><br>

<h2>Task 4: Configuring route tables</h2>
A route table contains a set of rules, called routes, that are used to determine where network traffic is directed. Each subnet in a VPC must be associated with a route table because the table controls the routing for the subnet. A subnet can only be associated with one route table at a time, but you can associate multiple subnets with the same route table.<br><br>

To use an internet gateway, a subnet's route table must contain a route that directs internet-bound traffic to the internet gateway. If a subnet is associated with a route table that has a route to an internet gateway, it is known as a public subnet.<br><br>

In this task, you will:
<ul><li>Create a public route table for internet-bound traffic
<li>Add a route to the route table to direct internet-bound traffic to the internet gateway
<li>Associate the public subnet with the new route table</li></ul><br>

15.In the left navigation pane, choose Route Tables.<br>
Several route tables are displayed, but there is only one route table associated with Lab VPC.<br>
This route table routes traffic locally, so it is called a private route table.<br><br>

16.Scroll to the right so that you can see the VPC  column, then expand the width of the column so that you can see which one is used by Lab VPC.<br><br>
17.Scroll back to the left and select  the route table that shows Lab VPC.<br>
<img src="https://i.imgur.com/kX7hfvx.png" width=60%><br>
18.In the Name column, choose ✎then enter the name Private Route Table and choose✅
<img src="https://i.imgur.com/lGP00MR.png" width=60%><br>
19.In the lower half of the page, choose the Routes tab.<br>
There is only one route. It shows that all traffic that is destined for 10.0.0.0/16 (which is the range of the Lab VPC) will be routed locally. This route allows all subnets in a VPC to communicate with each other.<br>
You will now create a new public route table to send public traffic to the internet gateway.<br>
<img src="https://i.imgur.com/x6lS6Z4.png" width=60%><br>
20.Choose Create route table and configure these settings:<br>
<ul><li>Name: Public Route Table
<li>VPC: Lab VPC
<li>Choose Create route table</li></ul>
<img src="https://i.imgur.com/jd1sQV2.png" width=60%><br>
21.In the Routes tab, choose Edit routes<br>
You will now add a route to direct internet-bound traffic (0.0.0.0/0) to the internet gateway.
<img src="https://i.imgur.com/10wUecW.png" width=60%><br>
22.Choose Add route then configure these settings:<br>
<ul><li>Destination: 0.0.0.0/0
<li>Target: Select Internet Gateway and then, from the list, select Lab IGW
<li>Choose Save changes</li></ul>
The last step is to associate this new route table with the public subnet.
<img src="https://i.imgur.com/KONHf1K.png" width=60%><br>
23.Choose the Subnet associations tab.<br><br>
24.Choose Edit subnet associations<br>
<img src="https://i.imgur.com/STnFypX.png" width=60%><br>
25.Select  the row with Public Subnet.<br><br>
26.Choose Save associations<br>
The public subnet is now public because it has a route table entry that sends traffic to the internet via the internet gateway.<br>
To summarize, you can create a public subnet by following these steps:<br>
<ul><li>Create an internet gateway
<li>Create a route table
<li>Add a route to the route table that directs 0.0.0.0/0 traffic to the internet gateway
<li>Associate the route table with a subnet, which thus becomes a public subnet</li></ul>
<img src="https://i.imgur.com/dnIrx5g.png" width=60%><br>

<h2>Task 5: Creating a security group for the application server</h2>
A security group acts as a virtual firewall for instances to control inbound and outbound traffic. Security groups operate at the level of the elastic network interface for the instance. Security groups do not operate at the subnet level. Thus, each instance can have its own firewall that controls traffic. If you do not specify a particular security group at launch time, the instance is automatically assigned to the default security group for the VPC.<br>
In this task, you will create a security group that allows users to access your application server via HTTP.<br><br>

27.In the left navigation pane, choose Security Groups.<br><br>

28.Choose Create security group and configure these settings:
<ul><li>Security group name: App-SG
<li>Description: Allow HTTP traffic
<li>VPC: select the X to clear the default selection, then choose Lab VPC
<li>Scroll to the bottom and choose Create security group</li></ul>
<img src="https://i.imgur.com/D7ptTBI.png" width=60%><br>
29.Verify the Inbound rules tab is selected below.<br>
The settings for Inbound Rules determine what traffic is permitted to reach the instance.<br>
You will configure it to permit HTTP (port 80) traffic that comes from anywhere on the internet (0.0.0.0/0).
<img src="https://i.imgur.com/6Ke07oT.png" width=60%><br>
30.Choose Edit inbound rules<br><br>
31.Choose Add rule and then configure these settings:
<ul><li>Type:  HTTP
<li>Source type: Anywhere-IPv4
<li>Description: Allow web access
<li>Choose Save rules</li></ul>
You use this App-SG in the next task.
<img src="https://i.imgur.com/vTB4IwR.png" width=60%><br>

<h2>Task 6: Launching an application server in the public subnet</h2>
To test that your VPC is correctly configured, you will now launch an EC2 instance into the public subnet. You will also confirm that you can access the EC2 instance from the internet.<br><br>

32.In the search box to the right of  Services, search for and choose EC2 to open the EC2 console.<br><br>

33.From the Launch instance menu, choose Launch Instance. Configure these options:
<ul><li>Name: App Server
<li>In the list of available Quick Start AMIs, keep the default Amazon Linux selected. Also keep the specific default Amazon Linux 2023 AMI  selected.
<li>In the Instance type panel, keep the default t2.micro selected.
<li>From the Key pair name menu, select vockey.
<li>Next to Network settings, choose Edit, then configure: 
<ul><li>Network: Lab VPC
<li>Subnet: Public Subnet</li></ul>

<li>Under Firewall (security groups), choose  Select an existing security group.
<ul><li>For Common security groups, select App-SG.</li></ul>
<li>In the Configure storage section, keep the default settings.
<li>Expand the Advanced details panel.
<li>IAM instance profile: Inventory-App-Role 
<li>Scroll to the bottom of the page and then copy and paste the code shown below into the User data box:
<pre class="text">
#!/bin/bash
# Install Apache Web Server and PHP
dnf install -y httpd wget php-fpm php-mysqli php-json php php-devel
dnf install -y mariadb105-server
# Download Lab files
wget https://aws-tc-largeobjects.s3-us-west-2.amazonaws.com/ILT-TF-200-ACACAD-20-EN/mod6-guided/scripts/inventory-app.zip
unzip inventory-app.zip -d /var/www/html/
# Download and install the AWS SDK for PHP
wget https://github.com/aws/aws-sdk-php/releases/download/3.62.3/aws.zip
unzip aws -d /var/www/html
# Turn on web server
chkconfig httpd on
service httpd start
</pre>
<li>At the bottom of the Summary panel on the right side of the screen choose Launch instanceYou will see a Success message.</li></ul>
<img src="https://i.imgur.com/NTbepFo.png" width=60%>
<img src="https://i.imgur.com/2iwDgOf.png" width=60%>
<img src="https://i.imgur.com/9lsZuA5.png" width=60%>
<img src="https://i.imgur.com/zKSq4E9.png" width=60%>
<img src="https://i.imgur.com/mlQpYdj.png" width=60%>
<img src="https://i.imgur.com/5z5FLHY.png" width=60%><br>
ec2-35-175-127-6.compute-1.amazonaws.com
<img src="https://i.imgur.com/8QhWLH7.png" width=60%><br>
<img src="https://i.imgur.com/PRxVAdO.png" width=60%><br>
