Image Resizer for AWS

-----------------------------------------------
Packaging the Lambda Function:
-----------------------------------------------

Install Dependencies Locally:

In your project directory, run:

npm init -y
npm install aws-sdk
npm install --platform=linux --arch=x64 --libc=glibc sharp
npm install --platform=linux --arch=x64 --libc=glibc



Zip the Code and Dependencies: Package all files into a .zip file to upload to AWS Lambda:
Compress-Archive -Path * -DestinationPath lambda-function.zip


--------------------------------
Important Considerations
--------------------------------


Triggers and Permissions: Ensure the Lambda function has the correct S3 bucket trigger and appropriate IAM role permissions to read from and write to the S3 bucket.
----------------------------
In Lambda console:
+ Add trigger
Select source: S3
Select the ARN of the bucket (the S3 bucket you are using)
Select "All Object Create Events" for Event Type
Set Prefix to: original-images/
Acknowledge Recursive Invocation warning (we are using a prefix to avoid recursive invocation)


Environment Setup: Make sure the sharp library and other dependencies are correctly included in the .zip package uploaded to Lambda.
-----------------------------


Setup Permissions for the lambda function:
-----------------------------
Within Lambda console, go to Configuration tab
Click Permissions in sidebar
Note the Role Name
Go to IAM dashboard - create new policy that grants read/write access to the S3 bucket that is the Lambda function trigger source.



Runtime Configuration: Choose the appropriate Node.js runtime (like Node.js 14.x) when creating the Lambda function.