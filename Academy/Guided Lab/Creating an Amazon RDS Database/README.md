<h1>Module 5 Guided Lab - Creating an Amazon RDS Database</h1>
<h2>Lab overview and objectives</h2>
FYI: <a href="https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html">What is Amazon Relational Database Service (Amazon RDS)?</a><br><br>

Traditionally, creating a database can be a complex process that requires either a database administrator or a systems administrator. In the cloud, you can simplify this process by using Amazon Relational Database Service (Amazon RDS).<br><br>
After completing this lab, you should be able to:<br>
<ul><li>Launch a database using Amazon RDS  
<li>Configure a web application to connect to the database instance</li></ul>
At the end of this lab, your architecture will look like the following example:<br>
<img src="https://i.imgur.com/SU3Va9D.png" width=60%>

<h2>Task 1: Creating an Amazon RDS database</h2>
In this task, you will create a MySQL database in your virtual private cloud (VPC). MySQL is a popular open source relational database management system (RDBMS), so there are no software licensing fees.<br><br>

‼️Windows Users: Use Chrome or Firefox as your web browser for this lab. The lab instructions are not compatible with Internet Explorer because of a difference in the Amazon RDS console.<br><br>

1.In the search box to the right of  Services, search for and choose RDS to open the RDS console.<br>
2.Choose Create database<br>
<img src="https://i.imgur.com/jYh0qkK.png" width=80%><br>
3.Under Engine options, select <code>MySQL</code>.<br>
The options include several use cases, ranging from enterprise-class databases to Dev/Test systems. In the options, you might notice Amazon Aurora. Aurora is a MySQL-compatible system that was re-architected for the cloud. If your company uses large-scale MySQL or PostgreSQL databases, Aurora can provide enhanced performance.<br>
<img src="https://i.imgur.com/e6puO9U.png" width=60%><br>
4.Set the templates and availability and durability options:<br>
<ul><li>Under the Templates section, select <code>Dev/Test</code>.
<li>Under the Availability and durability section, select <code>Single DB instance</code></li></ul>
Note: the default Multi-AZ deployment option automatically creates a replica of the database in a second Availability Zone for High Availability, however in this lab that is not needed.<br>
<img src="https://i.imgur.com/KYZ1Jhy.png" width=60%>
<img src="https://i.imgur.com/0XDJNm7.png" width=60%><br>
5.Under the Settings section, configure these options:
<ul><li>DB instance identifier: <code>inventory-db</code>
<li>Username: <code>admin</code>
<li>Password: <code>lab-password</code>
<li>Confirm password: <code>lab-password</code></li></ul>
<img src="https://i.imgur.com/Hj9zVc1.png" width=60%>
<img src="https://i.imgur.com/DDrzJ7x.png" width=60%><br>
6.Under the DB instance class section, configure these options:
<ul><li>Select <code>Burstable classes</code> (includes t classes).
<li>Select <code>db.t3.micro</code></li></ul>
<img src="https://i.imgur.com/zW9W6OQ.png" width=60%><br>
7.Under the Connectivity section, configure these options: 
<ul><li>Virtual Private Cloud (VPC): <code>Lab VPC</code>
<li>Existing VPC security groups: 
<ul><li>Choose <code>DB-SG</code>. It will be highlighted. 
<li><code>Remove</code> the default security group.</li></ul></li></ul>
<img src="https://i.imgur.com/RaZm2XM.png" width=60%>
<img src="https://i.imgur.com/dH5D813.png" width=60%><br>
8.Expand the Additional configuration panel, then configure these settings:
<ul><li>Initial database name: <code>inventory</code></li></ul>
  Note: This is the logical name of the database that will be used by the application.<br>
<ul><li><code>Clear</code> (turn off) the <code>Enable Enhanced monitoring</code> option</li></ul>
<img src="https://i.imgur.com/11RwQXF.png" width=60%>
<img src="https://i.imgur.com/ToZU6QX.png" width=60%>
💬Feel free to review the many other options displayed on the page, but leave them set to their default values. Options include automatic backups, the ability to export log files, and automatic version upgrades. The ability to activate these features through check boxes demonstrates the power of using a fully managed database solution instead of installing, backing up, and maintaining the database yourself.<br><br>

9.Choose <code>Create database</code> (at the bottom of the page).<br>
You should receive a message indicating that your database is being created.<br>
‼️If you receive an error message that mentions rds-monitoring-role, confirm that you have cleared (turned off) the Enhanced Monitoring option in the previous step, then try again.<br>
Before you continue to the next task, the database instance status must be Available. This process might take several minutes.
<img src="https://i.imgur.com/0PS43xl.png" width=60%><br>

<h2>Task 2: Configuring web application communication with a database instance</h2>
This lab automatically deployed an Amazon Elastic Compute Cloud (Amazon EC2) instance with a running web application.<br>
You must use the IP address of the instance to connect to the application.<br><br>
10.In the search box to the right of  Services, search for and choose <code>EC2</code> to open the EC2 console.<br><br>
11.In the left navigation pane, choose <code>Instances</code>.<br>
In the center pane, there should be a running instance that is named <code>App Server</code>.<br><br>
12.Select the App Server instance.<br><br>
13.In the Details tab, copy the <code>Public IPv4 address</code> to your clipboard.<br>
Tip: If you hover over the IP address, a copy  icon appears. To copy the displayed value, choose the icon.<br>
<img src="https://i.imgur.com/2xoSX2l.png" width=60%>
14.Open a new web browser tab, paste the IP address into the address bar, and then press <code>ENTER</code>.<br>
The web application should appear.<br>
It does not display much information because the application is <code>not yet connected to the database</code>.<br>
<img src="https://i.imgur.com/EYIuS6L.png" width=60%><br>
15.Choose <code>Settings</code>.<br>
You can now configure the application to use the RDS DB instance you created earlier.<br>
You will first retrieve the Database Endpoint so that the application knows how to connect to a database.<br>
<img src="https://i.imgur.com/Ci4hw3k.png" width=60%><br>
16.Return to the AWS Management Console, but do not close the application tab. (You will return to it soon.<br><br>
17.In the  Services search box, search for and choose <code>RDS</code> to open the RDS console.<br><br>
18.In the left navigation pane, choose <code>Databases</code>.<br><br>
19.Choose <code>inventory-db</code>.<br>
<img src="https://i.imgur.com/9wGihQN.png" width=60%><br>
20.Scroll to the <code>Connectivity & Security section</code> and copy the Endpoint to your clipboard.
It should look similar to this example: <code>inventory-db.crwxbgqad61a.rds.amazonaws.com</code>
21.Return to the browser tab with the Inventory application, and enter these values:
<ul><li>Endpoint: Paste the endpoint you copied earlier
<li>Database: <code>inventory</code>
<li>Username: <code>admin</code>
<li>Password: <code>lab-password</code>
<li>Choose <code>Save</code></li></ul>
The application will now connect to the database, load some initial data, and display information.<br>
<img src="https://i.imgur.com/t1KDnAb.png" width=60%>
<img src="https://i.imgur.com/LmYae1W.png" width=60%>
22. ➕Add inventory, 📝edit, and 🗑️delete inventory information by using the web application.<br>
The inventory information is stored in the Amazon RDS MySQL database that you created earlier in the lab.<br>
This means that any failure in the application server will not lose any data.<br>
It also means that multiple application servers can access the same data.<br><br>
23.Insert new records into the table. Ensure that the table has 5 or more inventory records before submitting your work.<br>
<img src="https://i.imgur.com/pfLra7F.png" width=60%>
🎊You have now successfully launched the application and connected it to the database!<br>
Optional: You can access the saved parameters in the Systems Manager console, under Parameter Store.<br>
<img src="https://i.imgur.com/x8z9Dso.png" width=60%><br>
