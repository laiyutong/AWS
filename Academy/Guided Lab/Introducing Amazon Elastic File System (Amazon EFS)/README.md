
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
<img src="https://i.imgur.com/LtB5IfI.png" width="60%"><br>
16. Scroll to the <code>Static website hosting</code> panel.<br>
17. Choose <code>Edit</code><br>
18. Configure the following settings:<br>
<ul><li>Static web hosting: Enable<br>
<li>Hosting type: <code>Host a static website</code><br>
<li>Index document: <code>index.html</code><br>
<li>Note: You must enter this value, even though it is already displayed.<br>
<li>Error document: <code>error.html</code></li></ul>
<img src="https://i.imgur.com/FSH4Wf7.png" width="60%"><br>
19. Choose <code>Save changes</code><br>
20. In the Static website hosting panel, choose the link under Bucket website endpoint.<br>
    You will receive a <code>403 Forbidden</code> message because the bucket permissions have not been configured yet.<br> 
    Keep this tab open in your web browser so that you can return to it later.<br>
    Your bucket has now been configured to host a static website.<br>
    <img src="https://i.imgur.com/sIlKWY4.png" width="60%"><br>
    <img src="https://i.imgur.com/kQHXVAu.png" width="60%"><br>

In this task, you will upload the files that will serve as your static website to the bucket.<br>
21. Right-click each of these links and download the files to your computer:<br>
<ul>Ensure that each file keeps the same file name, including the extension.<br>
<li><a href="https://github.com/laiyutong/AWS/blob/main/Academy/Guided%20Lab/Hosting%20a%20Static%20Website/index.html">index.html</a>
<li><a href="https://github.com/laiyutong/AWS/blob/main/Academy/Guided%20Lab/Hosting%20a%20Static%20Website/script.js">script.js</a>
<li><a href="https://github.com/laiyutong/AWS/blob/main/Academy/Guided%20Lab/Hosting%20a%20Static%20Website/style.css">style.css</a></li></ul>
22. Return to the Amazon <code>S3 console</code> and in the <code>website-<123></code> bucket you created earlier, choose the <code>Objects</code> tab.<br>
23. Choose <code>Upload</code><br>
24. Choose <code>Add files</code><br>
25. Locate and select the three files that you downloaded.<br>
26. If prompted, choose I acknowledge that existing objects with the same name will be overwritten.<br>
27. Choose <code>Upload</code><br>
<img src="https://i.imgur.com/xZCUthU.png" width="60%"><br>


<h2>Task 3: Enabling access to the objects</h2>
Objects that are stored in Amazon S3 are private by default. This ensures that your organization's data remains secure.<br>
In this task, you will make the uploaded objects publicly accessible.<br>
First, confirm that the objects are currently private.<br>

28. Return to the browser tab that showed the 403 Forbidden message.<br>
29. Refresh the webpage.<br>
    If you accidentally closed this tab, go to the Properties tab, and in the Static website hosting panel choose the Endpoint link again.<br>
    You should still see a 403 Forbidden message.<br>
    Analysis: This response is expected! This message indicates that your static website is being hosted by Amazon S3, but that the content is private.<br>
    You can make Amazon S3 objects public through two different ways:<br>
    <ul><li>To make either a whole bucket public, or a specific directory in a bucket public, use a bucket policy.
    <li>To make individual objects in a bucket public, use an access control list (ACL).</li></ul>
    It is normally safer to make individual objects public because this avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.<br>
    You will now configure the individual objects to be publicly accessible.<br>
30. Return to the web browser tab with the Amazon S3 console (but do not close the website tab).<br>
31. <code>Select all three objects</code>.<br>
32. In the Actions menu, choose <code>Make public via ACL</code>.<br>
<img src="https://i.imgur.com/NuHfCd5.png" width="60%"><br>
    A list of the three objects is displayed.<br>
33. Choose <code>Make public</code><br>
<img src="https://i.imgur.com/CYRkqvg.png" width="60%"><br>
    Your static website is now publicly accessible.<br>
34. Return to the web browser tab that has the 403 Forbidden message.<br>
35. Refresh the webpage.<br>
You should now see the static website that is being hosted by Amazon S3.<br>
<img src="https://i.imgur.com/at9azlT.png" width="60%"><br>

<h2>Task 4: Updating the website</h2>
You can change the website by editing the HTML file and uploading it again to the S3 bucket.<br>
Amazon S3 is an object storage service, so you must upload the whole file. This action replaces the existing object in your bucket. You cannot edit the contents of an object—instead, the whole object must be replaced.<br>

36. On your computer, load the index.html file into a text editor (for example, Notepad or TextEdit).<br>
37. Find the text <code>Served from Amazon S3</code> and replace it with <code>Created by &lt;YOUR-NAME&gt;</code>, substituting your name for <YOUR-NAME> (for example, Created by Jane).<br>
38. Save the file.<br>
39. Return to the Amazon S3 console and upload the <code>index.html</code> file that you just edited.<br>
40. <code>Select index.html</code> and use the Actions menu to choose the <code>Make public via ACL</code> option again.<br>
41. 
<img src="" width="60%"><br><br>

