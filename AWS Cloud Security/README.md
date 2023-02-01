<h1>AWS Cloud Security</h1>

<h2>AWS Global Infrastructure</h2>
<h4>AWS shared responsibility model</h4>
<img src="https://i.imgur.com/nxpbPhG.png" alt="responsability" width="80%">

<h2>AWS Identity and Access Management (IAM)</h2>
<h4>IAM Essential components</h4>
<ul>
<li>IAM user：<code>person</code> or <code>application</code><br>
<li>IAM group：<code>collection</code> of IAM users<br>
<li>IAM policy：The document that defines <code>which resources can be accessed</code> and the level of access to each resource.<br>
<li>IAM role：bounded to <code>IAM Policy</code> and have specific AWS resource access permissions<br>
</ul>

<h4>IAM policies type</h4>
<ul>
<li><code>Identity</code>-based：Attach a policy to any IAM <code>entity</code><br>
<li><code>Resource</code>-based：Attached to a <code>resource</code> (such as an S3 bucket)<br>
</ul>

<h4>Authenticate as an IAM user to gain access</h4>
<ul>
<li>Programmatic access：<code>Access key ID</code> / <code>Secret access key</code><br>
<li>AWS Management Console access：<code>12-digit Account ID or alias</code> / <code>IAM user name</code> / <code>IAM password</code><br>
</ul>

<h4>IAM Multi-factor Authentication(MFA)</h4>
<ul>
<li>MFA provides increased <code>security</code><br>
<li>requires a unique <code>authentication</code> code to access AWS services.<br>
</ul>

<h4>IAM Authorization</h4>
<ul>
<li>Assign permissions by creating an <code>IAM policy</code><br>
<li>Permissions determine <code>which resources and operations</code> are allowed<br>
<li>Best practice: Follow the principle of <code>least privilege</code><br>
</ul>
