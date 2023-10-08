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
In the AWS Management Console, on the Services menu, choose S3.<br>
Choose Create bucket<br>

An S3 bucket name is globally unique, and the namespace is shared by all AWS accounts. After you create a bucket, the name of that bucket cannot be used by another AWS account in any AWS Region unless you delete the bucket.

Thus, for this lab, you will use a bucket name that includes a random number, such as: website-123

For Bucket name, enter: website-<123> (replace <123> with a random number)

Public access to buckets is blocked by default. Because the files in your static website will need to be accessible through the internet, you must permit public access.

Verify the AWS Region is set to us-east-1 (if it is not, choose the us-east-1 Region)
<img src="https://i.imgur.com/70klToy.png">
In the Object Ownership section, select ACLs enabled, then verify Bucket owner preferred is selected.

Clear Block all public access, then select the box that states I acknowledge that the current settings may result in this bucket and the objects within becoming public.

Choose Create bucket.

You can use tags to add additional information to a bucket, such as a project code, cost center, or owner.

Choose the name of your new bucket.

Choose the  Properties tab.

Scroll to the Tags panel.

Choose Edit then Add tag and enter:

Key: Department
Value: Marketing
Choose Save changes to save the tag.

Next, you will configure the bucket for static website hosting.

Stay in the Properties console.

Scroll to the Static website hosting panel.

Choose Edit

Configure the following settings:

Static web hosting: Enable

Hosting type: Host a static website

Index document: index.html

Note: You must enter this value, even though it is already displayed.
Error document: error.html

Choose Save changes

In the Static website hosting panel, choose the link under Bucket website endpoint.

You will receive a 403 Forbidden message because the bucket permissions have not been configured yet. Keep this tab open in your web browser so that you can return to it later.

Your bucket has now been configured to host a static website.
