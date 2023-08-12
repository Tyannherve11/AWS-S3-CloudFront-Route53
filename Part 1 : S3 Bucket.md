## Part1: Serve the web app from the S3 bucket

In this part, we create a S3 bucket, put the code for our website, then configure the S3 bucket to serve our website from a bucket endpoint.

### 1- Create a S3 bucket in AWS
- In the Console Home of your AWS account, click on Services. Scrool down the list and select the Storage domain in the drop down then choose S3.
  This will lead you the S3 service dashboard.
On the left panel, click on Buckets then click on the button Create bucket
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/c9e8bafe-8fef-4fe1-8cce-5acfe579a6ce)

Now, fill the bucket details:
* bucket name: eg, webapp
* AWS region: US East-1

- select ##ACLs enabled parameter
- Uncheck the Block all public access button to create a public bucket
- Check the Acknowledgement box
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/4512e273-7f87-4112-954f-777ead0db71e)

- Then allow the other options as Default then click on Create Bucket

Once the bucket is created you'll see it listed on the S3 dashboard.

### 2- Create folder and add files to the bucket

Click ont he bucket name, then click on create folder to create a new folder in the bucket.
Set the folder name : eg, image

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/3712c904-966d-4071-b811-87922b22ecd1)

upload the files in the folder.
NB: s3 provides an URL to open your app
If you click on the object URL now, it will display an error message: ***Access Denied***
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/91fc211f-b56e-4a73-adb2-d79f392b11e5)


To solve that we need to modify the permissions on the file

Back to the object detail page, click on the **Permissions** tab then click on **Edit**
Check the **Read** permission button for Everyone and acknowledge it 
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/82895658-e2ef-44b3-abf2-49924336a5ce)

Scroll down and click on Save changes
Now, click on the Object URL in the Object overview details, the file content will be displayed.

### 3- Secure S3 bucket through IAM policies (setting public access on files)
We have uploaded the static files of our website to the amazon S3 we created, lets now make the files public so that anyone can access with a link And also set the IAM policies.

- On the S3 console click on the S3 you created

- Click on the **Permissions** tab then in the **Block public access** section, click on **Edit**

- Untick the **Block all public access** box and click on **Save changes**

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/9c5cecfe-5f19-4493-be48-c199c6161850)


Now to Bucket policy, click on Edit

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::bucket-name/*"
        }
    ]
}
```
**NB: Make sur eyou modify the bucket name**


### 4- Configure S3 bucket properties
Let's configure our S3 bucket so that we can access the static web pages.

You need to specify the default page and error page for your website.
From the S3 dashboard, click on the name of the bucket, then click on the Properties tab

* Scroll down to the **Static website hosting** section and click on its **Edit** button.

* Select **Enable** for Static website hosting.

* Also, select **Host a static website** for the **Hosting type**.
Enter the file for your Index document  and Error document. The Error document is optional. 

* I used **index.html** for both Index document and Error document.

* Scroll down and click on **Save Changes**.
