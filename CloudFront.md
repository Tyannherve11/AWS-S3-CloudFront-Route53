## Part 2: Serve content from S3 bucket with CloudFront

I this part, we create a CloudFront distribution that will be used to serve our website. Cloudfront will provide a **Distribution domain name** on which we will be able to access the website from the browser.

### 1- Create the CloudFront distribution
* From the **Services** drop-down, scroll down to **Networking & Content Delivery** section and right-click on **CloudFront** to open it in a new tab. This should take you to the **CloudFront dashboard**.

* Click on **Create Distribution**.

* Under the **Origin** settings section, click on the **Origin Domain Name** field and select the **S3 bucket** you created earlier. Then click on **Use website endpoint button**.
* In the **Origin Path** field, leave it blank.
* For the field **Enable Origin shield** , select **NO**

Scroll down to the **Default Cache Behavior** settings section. For **Viewer Protocol Policy**, select **Redirect HTTP to HTTPS**.


![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/014bec66-0738-48ee-9791-dedf6b2a9d39)


* In the **Web Application Firewall** section, choose Do not **enable security protections** just for the demo.

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/6961d12f-7c8b-4a18-8702-44fd66fe2cf1)

Next, scroll down to the  **Settings**. Inside the **Default Root Object field**, enter the filename at the root level, which should be your landing page. I used **index.html** as my **Default Root Object**.
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/1116f381-3d0a-4e63-8186-f0f6c239745f)

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/27be7bd2-b617-4357-bade-046277185b5a)


After the CloudFront distribution has been deployed, copy the **URL** from the **Domain Name** column and paste it into your browser.

NB: if you open the distribtion domain name while the distribution is still deploying, the page will display a message: **This site can't be reached**
