<h1>Configuring the aws s3 bucket</h1>
<br />

<p><b>Step 1 - </b>Create an account <a href="https://us-east-2.console.aws.amazon.com/console/home">console.aws.amazon.com</a></p>


<p>
  <b>Step 2 - </b>Create user on <a href="https://console.aws.amazon.com/iam/home?region=us-east-2#/users">console.aws.amazon.com</a>
<br />
<b>(OR)</b>
<br />
Once you have created the account Click on service > Security, Identity & Compliance > IAM
</p>


<p>
  <b>Step 3 - </b>Click on Users > Add User <br />
  Enter a new username(eg. testuser) and select Access types as <b>‘Programmatic access’</b>. Then click on Next Permission > Next review > Create User
</p>
<p>Note down your Access key ID and Secret access key and click on close.</p>


<p><b>Step 4 - </b>Now Click on the user created (eg. testuser)</p>
<p>Note down the ARN (eg. arn:aws:iam::414731926230:user/testuser)</p>


<p><b>Step 5 - </b>Then click on <b>Add inline policy</b></p>


<p>
  <b>Step 6 -</b> Click on JSON and add the below policy code
  <code>
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "s3:ListAllMyBuckets",
                    "s3:PutObject",
                    "s3:GetObject"
                ],
                "Resource": [
                    "arn:aws:s3:::*"
                ]
            }
        ]
    }
  </code>
</p>
<p>
  Then click on <b>Review Policy</b>, give it a name(eg. new-policy) and <b>Create Policy</b>.
</p>


<p><b>Step 7 - </b>Then Click on <b>Services(from the Navmenu) > S3</b></p>


<p><b>Step 8 - </b>Then click on <b>Create bucket</b></p>
<p>Enter a unique bucket name , select Region and then click on <b>Next</b>.Then <b>Create bucket</b></p>


<p>
  <b>Step 9 - </b>Then click on the newly created bucket and then click on <b>Permissions > Bucket Policy</b> <br />
  <b>Replacing the <i>Principal.AWS value</i> and <i>Resource value</i> which value you can see in the top.</b>
  <code>
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "AddCannedAcl",
                "Effect": "Allow",
                "Principal": {
                    "AWS": [
                        "arn:aws:iam::883235560421:user/orionfileuploads"
                    ]
                },
                "Action": [
                    "s3:PutObject",
                    "s3:PutObjectAcl"
                ],
                "Resource": [
                    "arn:aws:s3:::onclick/*"
                ],
                "Condition": {
                    "StringEquals": {
                        "s3:x-amz-acl": [
                            "public-read"
                        ]
                    }
                }
            }
        ]
    }
  </code>
</p>


<p>
  <b>Step 10 - </b>Now got <b>CORS configuration</b> and add this
  <code>
    <?xml version="1.0" encoding="UTF-8"?>
    <CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
      <CORSRule>
        <AllowedOrigin>*</AllowedOrigin>
        <AllowedMethod>GET</AllowedMethod>
        <AllowedMethod>POST</AllowedMethod>
        <AllowedMethod>PUT</AllowedMethod>
        <MaxAgeSeconds>3000</MaxAgeSeconds>
        <AllowedHeader>Authorization</AllowedHeader>
      </CORSRule>
    </CORSConfiguration>
  </code>
  then click <b>save</b>
</p>


<p>
  Yeah!!! It's Done <br />
  If you have any error, contact me
  <a href="https://www.facebook.com/pyaesonekhant.zeroboy">Facebook account</a>
</p>
