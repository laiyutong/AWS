
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
<img src="https://i.imgur.com/JFFitwT.png" width="60%"><br>
8. Choose Create security group then configure:<br>
<ul><li>Security group name: <code>EFS Mount Target</code>
<li>Description: <code>Inbound NFS access from EFS clients</code>
<li>VPC: Lab VPC</li></ul>
<img src="https://i.imgur.com/invpybj.png" width="60%"><br>
9. Under the Inbound rules section, choose Add rule then configure:
<ul><li>Type: NFS
<li>Source:
<ul><li>Custom
<li>In the Custom box, paste the security group's Security group ID that you copied to your text editor</li></ul>
<li>Choose Create security group.</li></ul>
<img src="https://i.imgur.com/7JvB5al.png" width="60%"><br>

<h2>Task 2: Creating an EFS file system</h2>
EFS file systems can be mounted to multiple EC2 instances that run in different Availability Zones in the same Region. These instances use mount targets that are created in each Availability Zone to mount the file system by using standard NFSv4.1 semantics. You can mount the file system on instances in only one virtual private cloud (VPC) at a time. Both the file system and the VPC must be in the same Region.<br>
10. On the Services menu, choose <code>EFS</code>.<br>
11. Choose <code>Create file system</code><br>
12. In the Create file system window, choose <code>Customize</code><br>
<img src="https://i.imgur.com/SrGHVyr.png" width="60%"><br>
13. On Step 1:<br>
<ul><li>Uncheck  Enable automatic backups.
<li>Lifecycle management: Select None
<li>In the Tags section, configure:
<ul><li>Key: Name
<li>Value: My First EFS File System</li></ul></li></ul><br>
<img src="https://i.imgur.com/Tv7MXQW.png" width="60%"><br>
14. Choose Next<br>
15. For VPC, select Lab VPC.<br>
16. Detach the default security group from each Availability Zone mount target by choosing the  check box on each default security group.<br>
17. Attach the EFS Mount Target security group to each Availability Zone mount target by:<br>
<ul><li>Selecting each Security groups check box.
<li>Choosing EFS Mount Target.</li></ul><br>
<img src="https://i.imgur.com/BJXNzhh.png" width="60%"><br>
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
△These instructions are specifically for Microsoft Windows users. If you are using <code>macOS or Linux</code>, skip to the next section.

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
<img src="https://i.imgur.com/DBLoUSj.png" width="60%"><br>
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
  <img src="https://i.imgur.com/erdCfUf.png" width="60%"><br>
38. When you are prompted to allow the first connection to this remote SSH server, enter yes.<br>
Because you are using a key pair for authentication, you are not prompted for a password.<br>
<h2>Task 4: Creating a new directory and mounting the EFS file system</h2>
△Amazon EFS supports the NFSv4.1 and NFSv4.0 protocols when it mounts your file systems on EC2 instances. Though NFSv4.0 is supported, we recommend that you use NFSv4.1. When you mount your EFS file system on your EC2 instance, you must also use an NFS client that supports your chosen NFSv4 protocol. The EC2 instance that was launched as a part of this lab includes an NFSv4.1 client, which is already installed on it.<br>
39. In your SSH session, make a new directory by entering <code>sudo mkdir efs</code><br>
40. Back in the AWS Management Console, on the Services menu, choose <code>EFS</code>.<br>
41. Choose My First EFS File System.<br>
42. In the Amazon EFS Console, on the top right corner of the page, choose Attach to open the Amazon EC2 mount instructions.<br>
43. Copy the entire command in the Using the NFS client section.<br>
  The mount command should look similar to this example:<br>
  <pre class="text">sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-bce57914.efs.us-west-2.amazonaws.com:/ efs</pre>
  The provided <code>sudo mount...</code> command uses the default Linux mount options.<br>
44. In your Linux SSH session, mount your Amazon EFS file system by:<br>
<ul><li>Pasting the command
<li>Pressing ENTER</li></ul>
45. Get a full summary of the available and used disk space usage by entering:<br>
<pre class="text">sudo df -hT</pre>
This following screenshot is an example of the output from the following disk filesystem command:<br>
<pre class="text">df -hT</pre>
Notice the Type and Size of your mounted EFS file system.

<h2>Task 5: Examining the performance behavior of your new EFS file system</h2>
<h3>Examining the performance by using Flexible IO</h3>
△Flexible IO (fio) is a synthetic I/O benchmarking utility for Linux. It is used to benchmark and test Linux I/O subsystems. During boot, fio was automatically installed on your EC2 instance.<br>
46. Examine the write performance characteristics of your file system by entering:<br>
<pre class="text">sudo fio --name=fio-efs --filesize=10G --filename=./efs/fio-efs-test.img --bs=1M --nrfiles=1 --direct=1 --sync=0 --rw=write --iodepth=200 --ioengine=libaio</pre>
△ The fio command will take 5–10 minutes to complete. The output should look like the example in the following screenshot. Make sure that you examine the output of your fio command, specifically the summary status information for this WRITE test.<br>
<h3>Monitoring performance by using Amazon CloudWatch</h3>
47. In the AWS Management Console, on the Services menu, choose CloudWatch.<br>
48. In the navigation pane on the left, choose Metrics.<br>
49. In the All metrics tab, choose EFS.<br>
50. Choose File System Metrics.<br>
51. Select the row that has the PermittedThroughput Metric Name.
△You might need to wait 2–3 minutes and refresh the screen several times before all available metrics, including PermittedThroughput, calculate and populate.<br>
52. On the graph, choose and drag around the data line. If you do not see the line graph, adjust the time range of the graph to display the period during which you ran the <code>fio</code> command.<br>
<img src="https://i.imgur.com/9tDS8wo.png" width="60%"><br>
53. Pause your pointer on the data line in the graph. The value should be 105M.<br>
<img src="https://i.imgur.com/cToVWmL.png" width="60%"><br>
The throughput of Amazon EFS scales as the file system grows. File-based workloads are typically spiky. They drive high levels of throughput for short periods of time, and low levels of throughput the rest of the time. Because of this behavior, Amazon EFS is designed to burst to high throughput levels for periods of time. All file systems, regardless of size, can burst to 100 MiB/s of throughput. For more information about performance characteristics of your EFS file system, see the official Amazon Elastic File System documentation.<br>
54. In the All metrics tab, uncheck the box for PermittedThroughput.<br>
55. Select the check box for DataWriteIOBytes.<br>
△ If you do not see DataWriteIOBytes in the list of metrics, use the File System Metrics search to find it.<br>
56. Choose the Graphed metrics tab.<br>
57. On the Statistics column, select Sum.<br>
58. On the Period column, select 1 Minute.<br>
59. Pause your pointer on the peak of the line graph. Take this number (in bytes) and divide it by the duration in seconds (60 seconds). The result gives you the write throughput (B/s) of your file system during your test.<br>
<img src="https://i.imgur.com/buJhWyl.png" width="60%"><br>
The throughput that is available to a file system scales as a file system grows. All file systems deliver a consistent baseline performance of 50 MiB/s per TiB of storage. Also, all file systems (regardless of size) can burst to 100 MiB/s. File systems that are larger than 1T B can burst to 100 MiB/s per TiB of storage. As you add data to your file system, the maximum throughput that is available to the file system scales linearly and automatically with your storage.<br>
File system throughput is shared across all EC2 instances that are connected to a file system. For more information about performance characteristics of your EFS file system, see the official Amazon Elastic File System documentation.<br>
🎊 Congratulations! You created an EFS file system, mounted it to an EC2 instance, and ran an I/O benchmark test to examine its performance characteristics.

<img src="" width="60%"><br>
<img src="" width="60%"><br>
<img src="" width="60%"><br>

