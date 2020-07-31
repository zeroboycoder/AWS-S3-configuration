<h1>Configuring the aws s3 bucket</h1>
<br />

<p><b>Step 1 - </b>Create an account <a href="https://us-east-2.console.aws.amazon.com/console/home">console.aws.amazon.com</a></p>
<br />

<p>
  <b>Step 2 - </b>Create user on <a href="https://console.aws.amazon.com/iam/home?region=us-east-2#/users">console.aws.amazon.com/iam/home</a>
<br />
<b>(OR)</b>
<br />
  Click on <b>service(from Navmenu) > Security, Identity & Compliance > IAM</b>
</p>
<br />

<p>
  <b>Step 3 - </b>Click on Users > Add User <br />
  Enter a new username(eg. testuser) and select Access types as <b>‘Programmatic access’</b>. Then click on Next Permission > Next review > Create User <br />
  Note down your Access key ID and Secret access key and click on close.</p>
<br />

<p><b>Step 4 - </b>Now Click on the user created (eg. testuser)</p>
<p>Note down the ARN (eg. arn:aws:iam::414731926230:user/testuser)</p>
<br />

<p><b>Step 5 - </b>Then click on <b>Add inline policy</b></p>
<br />

<p>
  <b>Step 6 -</b> Click on <b>JSON</b> and add the below policy code. Then click on <b>Review Policy</b>, give it a name(eg. new-policy) and <b>Create Policy</b>
  <pre>
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
  </pre>
</p>
<br />

<p><b>Step 7 - </b>Then Click on <b>Services(from the Navmenu) > S3</b></p>
<br />

<p><b>Step 8 - </b>Then click on <b>Create bucket</b></p>
<p>Enter a unique bucket name , select Region and then click on <b>Next</b>.Then <b>Create bucket</b></p>
<br />

<p>
  <b>Step 9 - </b>Then click on the newly created bucket and then click on <b>Permissions > Bucket Policy</b> <br />
  <b>Replacing the <u><i>Principal.AWS value</i></u> and <i><u>Resource value</u></i> which value you can see in the top.</b>
  <pre>
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
  </pre>
</p>
<br />

<p>
  <b>Step 10 - </b>Now got <b>CORS configuration</b> and add this
  <pre>
    <code>
        &lt;?xml version="1.0" encoding="UTF-8"?&gt;
        &lt;CORSConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/"&gt;
          &lt;CORSRule&gt;
            &lt;AllowedOrigin&gt;*&lt;/AllowedOrigin&gt;
            &lt;AllowedMethod&gt;GET&lt;/AllowedMethod&gt;
            &lt;AllowedMethod&gt;POST&lt;/AllowedMethod&gt;
            &lt;AllowedMethod&gt;PUT&lt;/AllowedMethod&gt;
            &lt;MaxAgeSeconds&gt;3000&lt;/MaxAgeSeconds&gt;
            &lt;AllowedHeader&gt;Authorization&lt;/AllowedHeader&gt;
          &lt;/CORSRule&gt;
        &lt;/CORSConfiguration&gt;
    </code>
  </pre>
  then click <b>save</b>
</p>
<br />

<p>
  Yeah!!! It's Done <br />
  If you have any error, contact me
  <a href="https://www.facebook.com/pyaesonekhant.zeroboy">Facebook account</a>
</p>
