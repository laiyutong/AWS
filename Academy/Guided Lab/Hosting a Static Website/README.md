<h1>Module 3 – Guided Lab: Hosting a Static Website</h1>
<h2>Lab overview and objectives</h2>
Static websites have fixed content with no backend processing. They can contain HTML pages, images, style sheets, and all files that are needed to render a website. However, static websites do not use server-side scripting or a database. If you want your static webpages to provide interactivity and run programming logic, you can use JavaScript that runs in the user's web browser.<br><br>

You can easily host a static website on Amazon Simple Storage Service (Amazon S3) by uploading the content and making it publicly accessible. No servers are needed, and you can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web.

After completing this lab, you should be able to:
<li>Create a bucket in Amazon S3
<li>Upload content to your bucket
<li>Enable access to the bucket objects
<li>Update the website

<h2>Task 1: Creating a bucket in Amazon S3</h2>
In this task, you will create an S3 bucket and configure it for static website hosting.<br>
5. In the AWS Management Console, on the <code>Services</code> menu, choose <code>S3</code>.<br>
6. Choose <code>Create bucket</code><br>
<ul><li>An S3 bucket name is globally unique, and the namespace is shared by all AWS accounts. After you create a bucket, the name of that bucket cannot be used by another AWS account in any AWS Region unless you delete the bucket.
Thus, for this lab, you will use a bucket name that includes a random number, such as: website-123</li></ul><br>

7. For Bucket name, enter: <code>website-<123></code> (replace <123> with a random number)<br>
Public access to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access.<br>
<ul><li>Verify the AWS Region is set to us-east-1 (if it is not, choose the us-east-1 Region)</li></ul><br>
<img src="https://i.imgur.com/70klToy.png" width="60%"><br>

8. In the Object Ownership section, select ACLs enabled, then verify Bucket owner preferred is selected.<br>
<img src="https://i.imgur.com/N45mlVz.png" width="60%"><br>
9. Clear Block all public access, then select the box that states I acknowledge that the current settings may result in this bucket and the objects within becoming public.<br>
<img src="https://i.imgur.com/Ar873yW.png" width="60%"><br>
10. Choose <code>Create bucket</code>.<br>
<ul><li>You can use tags to add additional information to a bucket, such as a project code, cost center, or owner.</li></ul><br>
11. Choose the name of your new bucket.<br>
12. Choose the  Properties tab.<br>
13. Scroll to the Tags panel.<br>
14. Choose Edit then Add tag and enter:<br>
<ul><li>Key: Department
<li>Value: Marketing</li></ul>
<img src="https://i.imgur.com/Uytzrpf.png" width="60%"><br>
14. Choose <code>Save changes</code> to save the tag.<br>
<ul><li>Next, you will configure the bucket for static website hosting.</li></ul><br>
15. Stay in the <code>Properties</code> console.<br>
<img src="https://i.imgur.com/LtB5IfI.png" width="60%"><br>
16. Scroll to the Static website hosting panel.<br>
17. Choose Edit<br>
18. Configure the following settings:<br>
<ul><li>Static web hosting: Enable<br>
<li>Hosting type: <code>Host a static website</code><br>
<li>Index document: <code>index.html</code><br>
<li>Note: You must enter this value, even though it is already displayed.<br>
<li>Error document: <code>error.html</code></li></ul>
<img src="https://i.imgur.com/FSH4Wf7.png" width="60%"><br>
19. Choose <code>Save changes</code><br>
20. In the Static website hosting panel, choose the link under Bucket website endpoint.<br>
<ul><li>You will receive a <code>403 Forbidden</code> message because the bucket permissions have not been configured yet. Keep this tab open in your web browser so that you can return to it later.<br>
Your bucket has now been configured to host a static website.</li></ul><br>
<img src="https://i.imgur.com/sIlKWY4.png" width="60%"><br>
<img src="https://i.imgur.com/kQHXVAu.png" width="60%"><br>

<h2>Task 2: Uploading content to your bucket</h2>
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
<li>To make individual objects in a bucket public, use an access control list (ACL).</li></ul><br>
It is normally safer to make individual objects public because this avoids accidentally making other objects public. However, if you know that the entire bucket contains no sensitive information, you can use a bucket policy.<br>
You will now configure the individual objects to be publicly accessible.<br>
Return to the web browser tab with the Amazon S3 console (but do not close the website tab).<br>
Select all three objects.<br>
In the Actions menu, choose Make public via ACL.<br>
A list of the three objects is displayed.<br>
Choose Make public<br>
Your static website is now publicly accessible.<br>
Return to the web browser tab that has the 403 Forbidden message.<br>
Refresh the webpage.<br>
You should now see the static website that is being hosted by Amazon S3.<br>

<img src="https://i.imgur.com/NuHfCd5.png" width="60%"><br>
<img src="https://i.imgur.com/CYRkqvg.png" width="60%"><br>
<img src="https://i.imgur.com/at9azlT.png" width="60%"><br>
