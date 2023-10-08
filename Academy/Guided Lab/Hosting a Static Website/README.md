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
You will receive a <code>403 Forbidden</code> message because the bucket permissions have not been configured yet. Keep this tab open in your web browser so that you can return to it later.<br>
Your bucket has now been configured to host a static website.<br>
<img src="https://i.imgur.com/sIlKWY4.png" width="60%"><br>
