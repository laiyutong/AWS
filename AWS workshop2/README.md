<h1>Deploy personal blog with AWS Elastic Beanstalk</h1>
<h2>Introduction of AWS services</h2>
<b>S3 Bucket</b>: Amazon Simple Storage Service (Amazon S3) is an <code>object</code> storage service offering industry-leading scalability, data availability, security, and performance.<br><br>
<b>DynamoDB</b>: Amazon DynamoDB is a fully managed <code>NoSQL</code> database service that provides fast and predictable performance with seamless scalability.<br><br>
<b>IAM</b>: AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. With IAM, you can centrally manage permissions that control which AWS resources users can access. You use IAM to control who is authenticated (signed in) and authorized (has permissions) to use resources.<br><br>
<b>Elastic Beanstalk</b>: With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud <code>without having to learn about the infrastructure</code> that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.<br>

<h2>Goal</h2>
<img src="https://i.imgur.com/dcVoZVU.png" width="60%">

<h2>Applied Learning with AWS Services</h2>
Create a DynamoDB table for storing blog data with the necessary attributes.
<img src="https://i.imgur.com/XX5LkEv.png" width="60%">
The table name is named <code>article</code>, and the partition key is named <code>articleId</code>, then click <code>Create table</code>.
<img src="https://i.imgur.com/iaMDuzN.png" width="60%">
Create a s3 bucket to store blog images or any other assets.
<img src="https://i.imgur.com/zvkCR8x.png" width="60%">
<img src="https://i.imgur.com/uVrcgXZ.png" width="60%">
Uncheck <code>Block all public access</code> and check <code>I acknowledge...</code>, then click <code>Create bucket</code>.<br><br>
By default, Amazon S3 blocks all public access to your buckets and their objects for security reasons. 
This is a good practice to prevent unintentional exposure of your data to the public.
When you uncheck "Block all public access" and acknowledge the associated warning, you are essentially configuring the bucket to allow public access. 
This means that objects within the bucket can be made public and accessible to anyone on the internet.
<img src="https://i.imgur.com/NXoSAeK.png" width="60%">
When using Amazon S3 and DynamoDB in AWS, it's crucial to set up access permissions using AWS Identity and Access Management (IAM). IAM allows you to control who has access to your AWS resources and what actions they can perform.<br><br>

Click the number 16 below <code>Roles</code>.<br>
<img src="https://i.imgur.com/nvHezH1.png" width="60%"><br>
Click <code>Create Role</code>.<br>
<img src="https://i.imgur.com/2JmkVVE.png" width="60%">
At Step 1, choose <code>EC2</code> for use case.
<img src="https://i.imgur.com/i7CoUY6.png" width="60%">
<img src="https://i.imgur.com/604fYkv.png" width="60%">
<img src="https://i.imgur.com/X8wo9hR.png" width="60%">
<img src="https://i.imgur.com/CPb4eu7.png" width="60%">
<img src="https://i.imgur.com/w5P0RXN.png" width="60%">
<img src="https://i.imgur.com/w92OZjI.png" width="60%">
<img src="https://i.imgur.com/vYaoNIX.png" width="60%">
<img src="https://i.imgur.com/fl8WlcG.png" width="60%">
<img src="https://i.imgur.com/7aOehp5.png" width="60%">
<img src="https://i.imgur.com/7MMXBlD.png" width="60%">
<img src="https://i.imgur.com/WRQqofe.png" width="60%">
<img src="https://i.imgur.com/i0ZLus5.png" width="60%">
<img src="" width="60%" alt="subnet">
<img src="https://i.imgur.com/2mqy5Cd.png" width="60%">
<img src="https://i.imgur.com/cKSkiaq.png" width="60%">
<img src="https://i.imgur.com/nWM3K73.png" width="60%">
<img src="https://i.imgur.com/bjjyH77.png" width="60%">
<img src="https://i.imgur.com/N3emkKk.png" width="60%">
<img src="https://i.imgur.com/27axbRx.png" width="60%">
<img src="https://i.imgur.com/wIJYLH7.png" width="60%">
<img src="https://i.imgur.com/KGVjVzr.png" width="60%">
<img src="https://i.imgur.com/VffA1qw.png" width="60%">
<img src="https://i.imgur.com/7lO0A7x.png" width="60%">
<img src="https://i.imgur.com/wUERYGs.png" width="60%">
<img src="https://i.imgur.com/kH4tqER.png" width="60%">
<img src="https://i.imgur.com/KvL2HiD.png" width="60%">
<pre class="text">
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::bucket_name/*"
            ]
        }
    ]
}
</pre>
<img src="https://i.imgur.com/YPDd8M8.png" width="60%">
<img src="https://i.imgur.com/a3kFhjQ.png" width="60%">
<img src="https://i.imgur.com/Vul5zOR.png" width="60%">
<img src="https://i.imgur.com/1cNEDJN.png" width="60%">
<img src="https://i.imgur.com/se5dnU2.png" width="60%">
<img src="https://i.imgur.com/AeCYI3i.png" width="60%">
<img src="https://i.imgur.com/3GH0L1J.png" width="60%">
<img src="https://i.imgur.com/kvqO3EM.png" width="60%">
<img src="https://i.imgur.com/rg6phIf.png" width="60%">
