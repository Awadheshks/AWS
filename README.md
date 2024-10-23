# Hosting a Resume on AWS Static Website

![Image](https://github.com/Awadheshks/assets/blob/b6db95ccc4fc4de034c4255a522ecc8adf7f3e74/StaticWebsite/AWS_StaticHosted_Arch.png)

Welcome to this tutorial! I'll guide you through hosting my own resume on AWS.

## Prerequisites
Before we dive in, make sure we do have the following:
- An AWS account
- Some HTML/CSS/JS knowledge to create our resume (or willing to learn)
- A local development environment (i.e., Visual Studio Code)
  
## Creating the Resume
  If you don't have a HTML/CSS/JS resume already, don't worry! There are several templates available that we can modify to create one. Once we've chosen a template, we can use a local IDE, like Visual Studio Code, to edit the code.

## Setting up S3 for Hosting
Amazon S3 is an excellent option for hosting static websites due to its robustness, scalability, and easy setup process. Here are the steps I followed to configure an S3 bucket for static website hosting:
  #### 1.	Create a new S3 bucket:
   Log into our AWS console and navigate to the S3 service. Click "Create bucket", enter a unique name for our
   bucket, and select a region.The rest of the settings can be left at their defaults, then just click "Create bucket" 
   at the very bottom.
    
![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Bucket-creation.png)

  #### 2.	Modify bucket policy to allow public read access:
   Uncheck “Block all public access” to allow public access of the bucket.
    
![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Bucket-policy.png)

  ### 3.	Enable static website hosting:
   After creating the bucket only, we can enable it for static hosting,so click on bucket name to open it. Under the
   "Properties" tab,at the very bottom you will find the."Static website hosting" section. Click "Edit", select "Enable",
   and then provide 'detailed-resume.html'as the "Index document" name and 'error.html' in the "Error document" field that
   I have created as a	custom error page.And then Click “Save Changes” to save the details
     
 ![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/StaticWebsite_hosting.png)


Now we have static website available

![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/StaticWebsite_url.png)

  When we click the URL, it throws ‘access denied’ error, even public access granted and static website enabled
![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Error-Accesdenied.png)

   So, we need to specify what kind of access people from internet should have. For that we need to scroll up and go to ‘Permissions” tab and edit Bucket policy.    
   What this policy is doing here is allowing to get object from ‘awadheshsinha.com’ Bucket.

![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Bucket_policy.png)

  #### 4.	Upload the website files:
   Now that the bucket is set up for hosting, I can upload my resume website files. For that go to the "Objects" tab and click "Upload". 
   We can drag and drop the files or click "Add files" to browse the file explorer. Click "Upload" to start the upload process. 

![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Files_upload.png)

  #### 5.	Test the website:
   Once the upload is complete, I can test my website. Navigate back to the "Properties" > "Static website hosting" 
   section and click on the URL in the "Endpoint" section. This should open my resume website in a new browser tab
   (many browsers will force you to acknowledge it's an HTTP website before viewing).
        http://awadheshsinha.com.s3-website-us-east-1.amazonaws.com/

 ![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Resume_screenshot.png)

 ## Setting up CloudFront Distribution
  CloudFront is a content delivery network (CDN) provided by AWS, which can serve our content from edge locations closer to our users,
  improving load times and providing a smoother user experience. To set up CloudFront distribution for our S3-hosted website, follow these steps:

#### 1.	Create a new CloudFront Distribution:
  Navigate to the CloudFront service from our AWS Management Console and click "Create a CloudFront Distribution".

#### 2.	Specify our S3 bucket as the origin:
   On the next page, you will be asked to specify the origin settings. For the "Origin Domain Name", you will see a 
   list of our S3 buckets. Select the bucket where you are hosting our resume website. Leave the "Origin ID" as it auto-fills.
![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Create_distribution.png)

   Scroll down to ‘Setting’ and enter Default toot object as ‘detailed-resume.html’.
![Image](https://github.com/Awadheshks/assets/blob/d9c4e2f9da0c5b82706e47484b98853dc838363d/StaticWebsite/Create_distribution_setting.png)

#### 3. Finally Test the website through CloudFront:
  Open newly created distributed domain name URL in any browser to view my resume.
          https://d3llgguvu0e6s7.cloudfront.net/









