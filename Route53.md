## Part 3: Serve the website using a custom domain name with Route 53

### 1 - Create yor domain name
It ca be done on any platform like google domain name, namecheap etc...

### 2- Link domain name to Route53

Route53 is a managed **DNS service** from AWS. It resolves domain names to its equivalent **IP address** from the domain provider. **Route53** also offers traffic management with various routing policies.

#### a- Create a Hosted zone in Route 53

To create a hosted zone, navigate to **AWS Console → Services → Route53 →  Hosted Zones** (in the left panel under Dashboard) and click on the **Create hosted zone** button. You would be prompted with the below screen.

* In the **Domain name** field, enter the domain name you registered 

* Set Type as **Public** and click on **Create hosted zone**

Once the hosted zone is created, you need to configure the name servers on your domain provider (Namecheap, google domain ...)  and link your domain name to **CloudFront.**

### b- Configure the nameservers in your domain name provider
To do that, follow the steps:

* On the **Hosted zones dashboard** click on the hosted zone you created 

* On the dashboard you will see the records created automatically by AWS when you created the hosted zone

* Select the record with type **NS**. On the side bar **Record details**, you will see the NS values that you will add to the namecheap name servers.

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/38c7eb5a-49da-4e51-ba78-0bf10cf4ed5e)

* Now, go to your provider , click on the **Manage** of your domain name.
* Then to ***NAMESERVER***
* select **custom DNS**
* Now copy and paste the nameservers from aws one after the other (Without the . at the end) then click on the tick to save.

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/7b0fb2d8-ac89-4b78-9375-566ae138882d)

***NB: It can take up  to 24hrs for the namesevers to propagate to aws route53***


Now we will secure the website ( for that, we will request a SSL certificate for the domain validation).

* Scroll down to Custom SSL and click on **Request certificate**

  on alternate the domain on cloudfront at the bottom
  ![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/e9ad1c2b-8d50-47e0-9326-7b4bd4849957)

  You will be taken to a new tab select R**equest a public certificate** then click **Next**

  ![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/0a44186a-fcb1-4cca-8fd1-105445116922)

  
 In the Domain names section, enter the domain name in the **Fully qualified domain name** field then scroll down and click on **Request** to create the certificate . 
**NB: The certificate can take up to 30 min to be created.**

  ![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/98548f1e-9d79-4ff9-9c16-b9dd0f32606e)

  You can click on **View certificate** to see the certificate details. The certificate shows **Pending** at the beginning and once it is **issued** the status changes to **issued**.

In the certificate you just created, scroll down to the **Domains** section and click on **Create records in Route 53**. 
  
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/cd95b517-febe-41e2-9c78-3cdefb2cfbb8)

Then click on the **Create records** button
Return to the previous tab from where you were redirected (Settings for the distribution) , select the certificate you just created  for the custom SSL and click on Save changes. 
![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/659fe662-5a48-400c-ad15-1d2b8eaee6b8)
After saving the changes, the distribution will be updated and the modifications will be deployed


### Setting records on route53 to direct traffic to cloudfront

In your domain hosted zones in **Route 53**, click s. on  **Create Record**.

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/02e3be63-161d-4198-ac42-6915c6f1fa5b)

We will be creating it as an A **record for IPv4** and we’ll select the **Alias** option.
In the **Alias Target (Route traffic to)**, select Alias to CloudFront distribution

Then, select your **CloudFront distribution** and click on **Create records**

![image](https://github.com/Tyannherve11/AWS-S3-CloudFront-Route53/assets/37128739/6507ab44-f09e-4082-b0b5-f925c4803d90)


Project completed!


