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
The private subnet will be used for resources that must remain isolated from the internet.<br><br>
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
<img src="https://i.imgur.com/OPW3fV2.png" width=60%><br>
<img src="https://i.imgur.com/QG6bhOK.png" width=60%><br>
<img src="https://i.imgur.com/HSMRj4Y.png" width=60%><br>
<img src="https://i.imgur.com/kX7hfvx.png" width=60%><br>
<img src="https://i.imgur.com/lGP00MR.png" width=60%><br>
<img src="https://i.imgur.com/x6lS6Z4.png" width=60%><br>
<img src="https://i.imgur.com/jd1sQV2.png" width=60%><br>
<img src="https://i.imgur.com/10wUecW.png" width=60%><br>
<img src="https://i.imgur.com/KONHf1K.png" width=60%><br>
<img src="https://i.imgur.com/STnFypX.png" width=60%><br>
<img src="https://i.imgur.com/dnIrx5g.png" width=60%><br>
<img src="https://i.imgur.com/D7ptTBI.png" width=60%><br>
<img src="https://i.imgur.com/6Ke07oT.png" width=60%><br>
<img src="https://i.imgur.com/vTB4IwR.png" width=60%><br>
<img src="https://i.imgur.com/g0N71kQ.png" width=60%><br>
<img src="https://i.imgur.com/NTbepFo.png" width=60%><br>
<img src="https://i.imgur.com/2iwDgOf.png" width=60%><br>
<img src="https://i.imgur.com/9lsZuA5.png" width=60%><br>
<img src="https://i.imgur.com/zKSq4E9.png" width=60%><br>
<img src="https://i.imgur.com/mlQpYdj.png" width=60%><br>
<img src="https://i.imgur.com/5z5FLHY.png" width=60%><br>
ec2-35-175-127-6.compute-1.amazonaws.com
<img src="https://i.imgur.com/8QhWLH7.png" width=60%><br>
<img src="https://i.imgur.com/PRxVAdO.png" width=60%><br>
