<h1>Sample Exam Questions</h1>

<h3>Question 1.</h3>
A company runs a public-facing three-tier web application in a VPC across multiple Availability Zones.<br> 
Amazon EC2 instances for the application tier running in <code>private</code> subnets need to download software patches from the <code>internet</code>.<br>
However, the EC2 instances <code>cannot be directly</code> accessible from the internet.<br><br>
Which actions should be taken to allow the EC2 instances to download the needed patches? (Select TWO.)<br>

<h3>Answer 1.</h3>
1. Configure a <code>NAT gateway</code> in a <code>public</code> subnet. <br>
2. Define a custom <code>route table</code> with a route to the NAT gateway for internet traffic and associate it with the 
private subnets for the application tier.<br>

<img src="https://i.imgur.com/veTSHOZ.png" alt="NAT" width="60%">

<h3>Question 2.</h3>
A SA wants to design a solution to <code>save costs</code> for Amazon EC2 instances that do not need to run during a 2-week company shutdown.<br>
The applications running on the EC2 instances store data in instance memory that must be <code>present when the instances resume operation</code>.<br><br>
Which approach should the solutions architect recommend to shut down and resume the EC2 instances?<br>

<h3>Answer 2.</h3>
Run the applications on EC2 instances enabled for <code>hibernation</code>.<br>
Hibernate the instances <code>before</code> the 2-week company shutdown. <br><br>

<b>FYI：</b><br>
When you hibernate an instance, Amazon EC2 signals the operating system to perform hibernation (suspend-to-disk).<br>
Hibernation saves the contents from the instance memory <code>(RAM)</code> to your Amazon Elastic Block Store <code>(Amazon EBS) root volume</code>.<br>
Amazon EC2 persists the instance's EBS root volume and any attached EBS data volumes. When you start your instance:
<ul>
<li>The EBS root volume is restored to its <code>previous state</code>
<li>The RAM contents are <code>reloaded</code>
<li>The processes that were <code>previously running</code> on the instance are resumed
<li>Previously attached data volumes are reattached and the instance retains its <code>instance ID</code>
</ul>

<h3>Question 3.</h3>
A company plans to run a monitoring application on an Amazon EC2 instance in a VPC.<br>
Connections are made to the EC2 instance using the instance’s private IPv4 address.<br>
A solutions architect needs to design a solution that will allow traffic to be quickly directed to a standby EC2 instance if the application 
fails and becomes unreachable.<br><br>
Which approach will meet these requirements?<br>

<h3>Answer 3.</h3>
Attach a secondary elastic network interface to the EC2 instance configured with the private IP address. <br>
Move the network interface to the standby EC2 instance if the primary EC2 instance becomes unreachable.<br>

<h3>Question 4.</h3>
An analytics company is planning to offer a web analytics service to its users.<br>
The service will require that the users’ webpages include a JavaScript script that makes authenticated GET requests to the 
company’s Amazon S3 bucket.<br><br>
What must a solutions architect do to ensure that the script will successfully execute?<br>

<h3>Answer 4.</h3>
Enable cross-origin resource sharing (CORS) on the S3 bucket.

<h3>Question 5.</h3>
A company’s security team requires that all data stored in the cloud be encrypted at rest at all times 
using encryption keys stored on premises.<br><br>
Which encryption options meet these requirements? (Select TWO.)<br>

<h3>Answer 5.</h3>
1. Use server-side encryption with customer-provided encryption keys (SSE-C).<br>
2. Use client-side encryption to provide at-rest encryption.<br>

<h3>Question 6.</h3>
A company uses Amazon EC2 Reserved Instances to run its data processing workload.<br>
The nightly job typically takes 7 hours to run and must finish within a 10-hour time window.<br>
The company anticipates temporary increases in demand at the end of each month that will cause the job to run over the time limit 
with the capacity of the current resources.<br>
Once started, the processing job cannot be interrupted before completion.<br>
The company wants to implement a solution that would provide increased resource capacity as cost-effectively as possible.<br><br>
What should a solutions architect do to accomplish this?<br>

<h3>Answer 6.</h3>
Deploy On-Demand Instances during periods of high demand.<br>

<h3>Question 7.</h3>
A company runs an online voting system for a weekly live television program.<br>
During broadcasts, users submit hundreds of thousands of votes within minutes to a front-end fleet of Amazon EC2 
instances that run in an Auto Scaling group.<br>
The EC2 instances write the votes to an Amazon RDS database.<br>
However, the database is unable to keep up with the requests that come from the EC2 instances.<br>
A solutions architect must design a solution that processes the votes in the most efficient manner and without downtime.<br><br>
Which solution meets these requirements?<br>

<h3>Answer 7.</h3>
Configure the front-end application to send votes to an Amazon Simple Queue Service (Amazon SQS) queue.<br>
Provision worker instances to read the SQS queue and write the vote information to the database.<br>

<h3>Question 8.</h3>
A company has a two-tier application architecture that runs in public and private subnets.<br>
Amazon EC2 instances running the web application are in the public subnet and an EC2 instance for the database runs 
on the private subnet.<br>
The web application instances and the database are running in a single Availability Zone (AZ).<br><br>
Which combination of steps should a solutions architect take to provide high availability for this 
architecture? (Select TWO.)<br>

<h3>Answer 8.</h3>
1. Create an Amazon EC2 Auto Scaling group and Application Load Balancer spanning multiple AZs for the 
web application instances.<br>
2. Create new public and private subnets in the same VPC, each in a new AZ.<br>
Create an Amazon RDS Multi-AZ DB instance in the private subnets. Migrate the old database contents to the new DB instance.

<h3>Question 9.</h3>
A website runs a custom web application that receives a burst of traffic each day at noon.<br>
The users upload new pictures and content daily, but have been complaining of timeouts.<br>
The architecture uses Amazon EC2 Auto Scaling groups, and the application consistently takes 1 minute to initiate upon boot 
up before responding to user requests.<br><br>
How should a solutions architect redesign the architecture to better respond to changing traffic?<br>

<h3>Answer 9.</h3>
Configure an Auto Scaling step scaling policy with an EC2 instance warmup condition.

<h3>Question 10.</h3>
An application running on AWS uses an Amazon Aurora Multi-AZ DB cluster deployment for its database.<br>
When evaluating performance metrics, a solutions architect discovered that the database reads 
are causing high I/O and adding latency to the write requests against the database.<br><br>
What should the solutions architect do to separate the read requests from the write requests?<br>

<h3>Answer 10.</h3>
Create an Aurora replica and modify the application to use the appropriate endpoints.

