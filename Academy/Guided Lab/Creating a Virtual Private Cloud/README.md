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
<img src="https://i.imgur.com/CoOmBZO.png" width=40%>
<img src="https://i.imgur.com/mq6qK21.png" width=60%>
<img src="https://i.imgur.com/vKTEUWa.png" width=60%>
<img src="https://i.imgur.com/c50hKar.png" width=60%>

<h2>Task 2: Creating subnets</h2>
<img src="https://i.imgur.com/aWrVzIT.png" width=40%>
<img src="https://i.imgur.com/2kCtMb6.png" width=60%>
<img src="https://i.imgur.com/PQ4iwzi.png" width=60%>
<img src="https://i.imgur.com/jJMQ3id.png" width=60%>
<img src="https://i.imgur.com/am8OtVl.png" width=60%>
<img src="https://i.imgur.com/iuwCrwB.png" width=60%>
<img src="https://i.imgur.com/PQ4iwzi.png" width=60%>
<img src="https://i.imgur.com/Wp3k4yA.png" width=60%>
<img src="https://i.imgur.com/OPW3fV2.png" width=60%>
<img src="https://i.imgur.com/QG6bhOK.png" width=60%>
<img src="https://i.imgur.com/HSMRj4Y.png" width=60%>
<img src="https://i.imgur.com/kX7hfvx.png" width=60%>
<img src="https://i.imgur.com/lGP00MR.png" width=60%>
<img src="https://i.imgur.com/x6lS6Z4.png" width=60%>
<img src="https://i.imgur.com/jd1sQV2.png" width=60%>
<img src="https://i.imgur.com/10wUecW.png" width=60%>
<img src="https://i.imgur.com/KONHf1K.png" width=60%>
<img src="https://i.imgur.com/STnFypX.png" width=60%>
<img src="https://i.imgur.com/dnIrx5g.png" width=60%>
<img src="https://i.imgur.com/D7ptTBI.png" width=60%>
<img src="https://i.imgur.com/6Ke07oT.png" width=60%>
<img src="https://i.imgur.com/vTB4IwR.png" width=60%>
<img src="https://i.imgur.com/g0N71kQ.png" width=60%>
<img src="https://i.imgur.com/NTbepFo.png" width=60%>
<img src="https://i.imgur.com/2iwDgOf.png" width=60%>
<img src="https://i.imgur.com/9lsZuA5.png" width=60%>
<img src="https://i.imgur.com/zKSq4E9.png" width=60%>
<img src="https://i.imgur.com/mlQpYdj.png" width=60%>
<img src="https://i.imgur.com/5z5FLHY.png" width=60%>
ec2-35-175-127-6.compute-1.amazonaws.com
<img src="https://i.imgur.com/8QhWLH7.png" width=60%>
<img src="https://i.imgur.com/PRxVAdO.png" width=60%>
