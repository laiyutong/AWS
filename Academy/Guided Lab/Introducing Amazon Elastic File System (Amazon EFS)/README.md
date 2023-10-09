
<h1>Module 4 - Guided Lab: Introducing Amazon Elastic File System (Amazon EFS)</h1>
<h2>Lab overview and objectives</h2>
This lab introduces you to Amazon Elastic File System (Amazon EFS) by using the AWS Management Console.<br>
After completing this lab, you should be able to:<br>
<ul><li>Log in to the AWS Management Console
<li>Create an Amazon EFS file system
<li>Log in to an Amazon Elastic Compute Cloud (Amazon EC2) instance that runs Amazon Linux
<li>Mount your file system to your EC2 instance
<li>Examine and monitor the performance of your file system</li></ul>


<h2>Task 1: Creating a security group to access your EFS file system</h2>
The security group that you associate with a mount target must allow inbound access for TCP on port 2049 for Network File System (NFS). This is the security group that you will now create, configure, and attach to your EFS mount targets.<br>

5. In the AWS Management Console, on the Services menu, choose <code>EC2</code>.
6. In the navigation pane on the left, choose <code>Security Groups</code>.
7. Copy the Security group ID of the EFSClient security group to your text editor.<br>
  The Group ID should look similar to sg-03727965651b6659b.<br>

8. Choose Create security group then configure:<br>
<ul><li>Security group name: EFS Mount Target
<li>Description: Inbound NFS access from EFS clients
<li>VPC: Lab VPC</li></ul><br>
9. Under the Inbound rules section, choose Add rule then configure:
<ul><li>Type: NFS
<li>Source:
<ul><li>Custom
<li>In the Custom box, paste the security group's Security group ID that you copied to your text editor</li></ul>
<li>Choose Create security group.</li></ul><br>

<h2>Task 2: Creating an EFS file system</h2>
EFS file systems can be mounted to multiple EC2 instances that run in different Availability Zones in the same Region. These instances use mount targets that are created in each Availability Zone to mount the file system by using standard NFSv4.1 semantics. You can mount the file system on instances in only one virtual private cloud (VPC) at a time. Both the file system and the VPC must be in the same Region.<br>
10. On the Services menu, choose <code>EFS</code>.<br>
11. Choose <code>Create file system</code><br>
12. In the Create file system window, choose <code>Customize</code><br>
13. On Step 1:<br>
<ul><li>Uncheck  Enable automatic backups.
<li>Lifecycle management: Select None
<li>In the Tags section, configure:
<ul><li>Key: Name
<li>Value: My First EFS File System</li></ul></li></ul><br>
14. Choose Next<br>
15. For VPC, select Lab VPC.<br>
16. Detach the default security group from each Availability Zone mount target by choosing the  check box on each default security group.<br>
17. Attach the EFS Mount Target security group to each Availability Zone mount target by:<br>
<ul><li>Selecting each Security groups check box.
<li>Choosing EFS Mount Target.</li></ul><br>
A mount target is created for each subnet.<br>
Your mount targets should look like the following example. The diagram shows two mount targets in the Lab VPC that use the EFS Mount Target security group. In this lab, you should be using the Lab VPC.<br>
18. Choose <code>Next</code><br>
19. On Step 3, Choose <code>Next</code><br>
20. IOn Step 4:<br>
<ul><li>Review your configuration.
<li>Choose Create</li></ul>
🎊Congratulations! You have created a new EFS file system in your Lab VPC and mount targets in each Lab VPC subnet. In a few seconds, the File system state of the file system will change to Available, followed by the mount targets 2–3 minutes later.<br><br>
Proceed to the next step after the Mount target state for each mount target changes to Available. Choose the screen refresh button after 2–3 minutes to check its progress.<br><br>
🗒️Note: You may need to scroll to the right in the File systems pane to find the File system state.<br>

<h2>Task 3: Connecting to your EC2 instance via SSH</h2>
In this task, you will connect to your EC2 instance by using Secure Shell (SSH).<br>
<h3>Microsoft Windows users</h3>
△These instructions are specifically for Microsoft Windows users. If you are using macOS or Linux, skip to the next section.

21. Above these instructions that you are currently reading, choose the Details dropdown menu, and then select <code>Show</code><br>
   A Credentials window opens.<br>
22. Choose the Download PPK button and save the labsuser.ppk file.
   Note: Typically, your browser saves the file to the Downloads directory.<br>
23. Note the EC2PublicIP address, if it is displayed.<br>
24. Exit the Details panel by choosing the X.<br>
25. To use SSH to access the EC2 instance, you must use *PuTTY*. If you do not have PuTTY installed on your computer, download PuTTY.<br>
26. Open putty.exe.<br>
27. To keep the PuTTY session open for a longer period of time, configure the PuTTY timeout:><br>
<ul><li>Choose Connection
<li>Seconds between keepalives: 30</li></ul><br>
28. Configure your PuTTY session by using the following settings.
<ul><li>Choose Session
<li>Host Name (or IP address): Paste the EC2PublicIP for the instance you noted earlier
<ul><li>Alternatively, return to the Amazon EC2 console and choose Instances
<li>Select the instance you want to connect to
<li>In the Description tab, copy the IPv4 Public IP value</li></ul>
<li>Back in PuTTY, in the Connection list, expand  SSH
<li>Choose Auth and expand  Credentials
<li>Under Private key file for authentication: Choose Browse
<li>Browse to the labsuser.ppk file that you downloaded, select it, and choose Open
<li>Choose Open again</li></ul><br>
29. To trust and connect to the host, choose Accept.<br>
30. When you are prompted with login as, enter: ec2-user
  This action connects you to the EC2 instance.<br>

<h3>macOS  and Linux  users</h3>
These instructions are specifically for macOS or Linux users. If you are a Windows user, skip ahead to the next task.<br>
31. Above these instructions that you are currently reading, choose the Details dropdown menu, and then select Show
  A Credentials window opens.<br>
32. Choose the Download PEM button and save the labsuser.pem file.<br>
33. Note the EC2PublicIP address, if it is displayed.<br>
34. Exit the Details panel by choosing the X.<br>
35. Open a terminal window, and change directory to the directory where the labsuser.pem file was downloaded by using the cd command.
    For example, if the labsuser.pem file was saved to your Downloads directory, run this command:<br>
<pre class="text">cd ~/Downloads</pre>
36. Change the permissions on the key to be read-only, by running this command:<br>
<pre class="text">chmod 400 labsuser.pem</pre>
37. Run the following command (replace <public-ip> with the EC2PublicIP address that you copied earlier).
<ul><li>Alternatively, to find the IP address of the on-premises instance, return to the Amazon EC2 console and select Instances
<li>Select the instance that you want to connect to
<li>In the Description tab, copy the IPv4 Public IP value</li></ul>
<pre class="text">ssh -i labsuser.pem ec2-user@<public-ip></pre><br>
38. When you are prompted to allow the first connection to this remote SSH server, enter yes.<br>
Because you are using a key pair for authentication, you are not prompted for a password.<br>
39. Return to the Amazon S3 console and upload the <code>index.html</code> file that you just edited.<br>
40. <code>Select index.html</code> and use the Actions menu to choose the <code>Make public via ACL</code> option again.<br>
41. 
<img src="" width="60%"><br><br>
<h2>Task 4: Updating the website</h2>
You can change the website by editing the HTML file and uploading it again to the S3 bucket.<br>
Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object—instead, the whole object must be replaced.<br>

