<h1>Sample Exam Questions</h1>

<h3>Question 1.</h3>
A company runs a public-facing three-tier web application in a VPC across multiple Availability Zones.<br> 
Amazon EC2 instances for the application tier running in private subnets need to download software patches from the internet.<br>
However, the EC2 instances cannot be directly accessible from the internet.<br><br>
Which actions should be taken to allow the EC2 instances to download the needed patches? (Select TWO.)<br>

<h3>Answer 1.</h3>
1. Configure a NAT gateway in a public subnet. <br>
2. Define a custom route table with a route to the NAT gateway for internet traffic and associate it with the 
private subnets for the application tier.<br>

<h3>Question 2.</h3>
A SA wants to design a solution to save costs for Amazon EC2 instances that do not 
need to run during a 2-week company shutdown.<br>
The applications running on the EC2 instances store data in instance memory that must be present when the instances resume operation.<br><br>
Which approach should the solutions architect recommend to shut down and resume the EC2 instances?<br>

<h3>Answer 2.</h3>
Run the applications on EC2 instances enabled for hibernation. Hibernate the instances before the 2-
week company shutdown. <br>

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
<h3>Answer 7.</h3>

<h3>Question 8.</h3>
<h3>Answer 8.</h3>

<h3>Question 9.</h3>
<h3>Answer 9.</h3>

<h3>Question 10.</h3>
<h3>Answer 10.</h3>
