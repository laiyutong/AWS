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
<img src="https://i.imgur.com/XX5LkEv.png" width="60%"><br>
The table name is named <code>article</code>, and the partition key is named <code>articleId</code>, then click <code>Create table</code>.
<img src="https://i.imgur.com/iaMDuzN.png" width="60%"><br>

Amazon S3 (Simple Storage Service) is a scalable and durable object storage service by AWS, designed to store and retrieve any type of data, from static website content and media files to backups, log files, and large datasets, providing reliable and cost-effective storage in the cloud.<br><br>
An S3 bucket is a fundamental container within the S3 service. It is used to store and organize objects, which can be files, documents, images, or any other type of data. Buckets have a globally unique name within S3, and objects stored within a bucket are identified by a unique key.<br><br>
Create a s3 bucket to store blog images or any other assets.
<img src="https://i.imgur.com/zvkCR8x.png" width="60%"><br>
<img src="https://i.imgur.com/uVrcgXZ.png" width="60%"><br>
Uncheck <code>Block all public access</code> and check <code>I acknowledge...</code>, then click <code>Create bucket</code>.<br><br>
By default, Amazon S3 blocks all public access to your buckets and their objects for security reasons. 
This is a good practice to prevent unintentional exposure of your data to the public.
When you uncheck "Block all public access" and acknowledge the associated warning, you are essentially configuring the bucket to allow public access. 
This means that objects within the bucket can be made public and accessible to anyone on the internet.<br>
<img src="https://i.imgur.com/NXoSAeK.png" width="60%"><br>
When using Amazon S3 and DynamoDB in AWS, it's crucial to set up access permissions using AWS Identity and Access Management (IAM). IAM allows you to control who has access to your AWS resources and what actions they can perform.<br><br>

Click the number 16 below <code>Roles</code>.<br>
<img src="https://i.imgur.com/nvHezH1.png" width="60%"><br>
Click <code>Create Role</code>.<br>
<img src="https://i.imgur.com/2JmkVVE.png" width="60%"><br>
At Step 1, choose <code>EC2</code> for use case.<br>
<img src="https://i.imgur.com/i7CoUY6.png" width="60%"><br>
At Step 2, add <code>AmazonS3FullAccess</code> for permission policies.<br>
<img src="https://i.imgur.com/604fYkv.png" width="60%"><br>
Add <code>AmazonDynamoDBFullAccess</code> for permission policies.<br>
<img src="https://i.imgur.com/X8wo9hR.png" width="60%"><br>
At Step 3, enter <code>Role name</code>, then click <code>Create Role</code>.<br>
<img src="https://i.imgur.com/CPb4eu7.png" width="60%"><br>
<img src="https://i.imgur.com/7aOehp5.png" width="60%"><br><br>
In AWS Elastic Beanstalk, creating an application involves setting up an environment to deploy and run your application.<br> 
Click <code>Create Application</code>.<br>
<img src="https://i.imgur.com/w5P0RXN.png" width="60%"><br>
Enter the <code>environment name</code>.<br>
<img src="https://i.imgur.com/w92OZjI.png" width="60%"><br>
When you use AWS Elastic Beanstalk and choose the platform "Java with Corretto 17 on Linux 2," it indicates the runtime environment and underlying infrastructure for your Java application. Let's break down the components:
<pre class="text">
Java:
Runtime Environment: Your application will run on the Java Virtual Machine (JVM). This is a standard Java runtime environment that allows you to execute Java applications.

Corretto 17:
Java Distribution: Amazon Corretto is a no-cost, multiplatform, production-ready distribution of the Open Java Development Kit (OpenJDK). In this case, "Corretto 17" refers to Java 17, which is a long-term support (LTS) version. LTS versions receive updates and support for an extended period.

Linux 2:
Operating System: Your application will run on Amazon Linux 2, which is the latest version of Amazon's Linux distribution. It provides a secure, stable, and high-performance execution environment for applications.</pre>
<img src="https://i.imgur.com/vYaoNIX.png" width="60%"><br>
Select to <code>upload your code</code>, the version label can be filled in <code>v0.0.1</code>, select <code>local file</code> and upload the <code>zip</code> file (no need to unzip).
<img src="https://i.imgur.com/fl8WlcG.png" width="60%"><br>
Then click <code>Next</code>.<br>
<img src="https://i.imgur.com/7MMXBlD.png" width="60%"><br><br>
After setting up an AWS Elastic Beanstalk environment, it's essential to configure permissions to ensure that the environment and associated AWS resources have the necessary access.<br><br>
Select <code>Use an existing service role</code> for Service role.<br>
Select the Role you just set for roles.<br>
Select the <code>default</code> for EC2 key pair.<br>
Select the same Role for EC2 Instance Profile.<br>
<img src="https://i.imgur.com/WRQqofe.png" width="60%"><br>
Select the <code>default</code> VPC and <code>activated</code> public IP.<br>
Select <code>all</code> subnets.<br>
<img src="https://i.imgur.com/i0ZLus5.png" width="60%"><br>
<code>Skip</code> step four and click <code>next</code> to go to step five.<br>
<img src="https://i.imgur.com/2mqy5Cd.png" width="60%"><br>
Scroll down to find <code>Environment properties</code>, click <code>add environment property</code>.<br>
Fill in <code>AWS_S3_BUCKET_NAME</code>: <code>your bucket name</code>, and <code>SERVER_PORT</code>: <code>5000</code>.<br>
<img src="https://i.imgur.com/cKSkiaq.png" width="60%"><br>
Then click <code>submit</code>. You may need to wait for a while to create an application.<br>
<img src="https://i.imgur.com/nWM3K73.png" width="60%"><br>
Go to the s3 bucker you just created and click <code>upload</code>.<br>
<img src="https://i.imgur.com/bjjyH77.png" width="60%"><br>
Click <code>Add files</code> to upload your files, such as index.html, style.css.<br>
<img src="https://i.imgur.com/N3emkKk.png" width="60%"><br>
<img src="https://i.imgur.com/27axbRx.png" width="60%"><br>

To make the files you uploaded to an Amazon S3 bucket accessible to everyone, you need to configure the appropriate permissions and set up the necessary configurations for hosting content.<br><br>
Click <code>properties</code>.<br>
<img src="https://i.imgur.com/wIJYLH7.png" width="60%"><br>
Scroll down to find <code>Static website hosting</code>, then click <code>edit</code>.<br>
<img src="https://i.imgur.com/KGVjVzr.png" width="60%"><br>
Static website hosting select <code>Enable</code>, enter <code>index.html</code> under index document, and then click <code>Save Change</code>.<br>
<img src="https://i.imgur.com/VffA1qw.png" width="60%"><br>
After saving changes, click on the generated URL, and you will see a 403 error message.<br>
<img src="https://i.imgur.com/7lO0A7x.png" width="60%"><br>
If you are encountering a 403 error (Forbidden) when trying to access a URL generated by an Amazon S3 bucket, it indicates that the requester (typically a user or application) does not have the necessary permissions to perform the requested action on the specified S3 object.<br> 
<img src="https://i.imgur.com/wUERYGs.png" width="60%"><br>
To solve the 403 forbidden error, click <code>permissions</code> and scroll down to find the <code>bucket policy</code>.<br> 
<img src="https://i.imgur.com/kH4tqER.png" width="60%"><br>
<img src="https://i.imgur.com/KvL2HiD.png" width="60%"><br>
Paste the following content and change the <code>bucket name</code>.<br>
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
<img src="https://i.imgur.com/YPDd8M8.png" width="60%"><br>
This policy grants public read access to objects (files) within a specific S3 bucket. Let's break down each component:
<pre class="text">
<b>Version</b>: Specifies the version of the policy language. In this case, it's set to "2012-10-17," indicating the version of the policy language used.

<b>Statement</b>: Defines the permissions in the policy. In this example, there is one statement within an array.

<b>Sid</b>: A human-readable identifier for the statement. In this case, it's named "PublicReadGetObject."

<b>Effect</b>: Specifies whether the statement allows or denies access. The value "Allow" indicates that the statement allows the specified actions.

<b>Principal</b>: Identifies the AWS entity (user, role, or account) to which the policy is attached. The wildcard * represents any AWS principal, meaning it allows access to any entity.

<b>Action</b>: Lists the specific actions (API operations) allowed or denied by the statement. Here, it allows the "s3:GetObject" action, which permits retrieving (reading) objects from the S3 bucket.

<b>Resource</b>: Specifies the AWS resource to which the statement applies. In this case, it specifies a resource ARN (Amazon Resource Name) for objects within the specified S3 bucket. The wildcard * at the end means it applies to any object within the bucket.
</pre>
Go to environment of elastic beanstalk.<br>
<img src="https://i.imgur.com/1cNEDJN.png" width="60%"><br>
<img src="https://i.imgur.com/Vul5zOR.png" width="60%"><br>
<img src="https://i.imgur.com/a3kFhjQ.png" width="60%"><br>
<img src="https://i.imgur.com/se5dnU2.png" width="60%"><br>
<img src="https://i.imgur.com/AeCYI3i.png" width="60%"><br>
<img src="https://i.imgur.com/3GH0L1J.png" width="60%"><br>
<img src="https://i.imgur.com/kvqO3EM.png" width="60%"><br>
<img src="https://i.imgur.com/rg6phIf.png" width="60%"><br>
