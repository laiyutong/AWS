<h1>Deploy personal blog with AWS Elastic Beanstalk</h1>
<h2>Introduction of AWS services</h2>
<b>S3 Bucket</b>: Amazon Simple Storage Service (Amazon S3) is an object storage service offering industry-leading scalability, data availability, security, and performance.<br>
<b>DynamoDB</b>: Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability.<br>
<b>Elastic Beanstalk</b>: With Elastic Beanstalk, you can quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. Elastic Beanstalk reduces management complexity without restricting choice or control. You simply upload your application, and Elastic Beanstalk automatically handles the details of capacity provisioning, load balancing, scaling, and application health monitoring.<br>

<img src="https://i.imgur.com/dcVoZVU.png" width="60%">

<img src="https://i.imgur.com/XX5LkEv.png" width="60%">
<img src="https://i.imgur.com/iaMDuzN.png" width="60%">
<img src="https://i.imgur.com/zvkCR8x.png" width="60%">
<img src="https://i.imgur.com/uVrcgXZ.png" width="60%">
<img src="https://i.imgur.com/NXoSAeK.png" width="60%">
<img src="https://i.imgur.com/nvHezH1.png" width="60%">
<img src="https://i.imgur.com/2JmkVVE.png" width="60%">
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
