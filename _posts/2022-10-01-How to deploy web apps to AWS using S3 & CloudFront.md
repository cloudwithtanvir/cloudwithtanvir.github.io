---
layout: post
title: How to deploy React/Vue/Svelte based webapp to AWS using S3 & CloudFront
categories: [AWS, S3, Cloudfront]
tags: [AWS, Amazon Web service, Cloudfront ,S3]
---




## How to deploy React/Vue/Svelte based webapp to AWS using S3 & CloudFront


# What is CloudFront:

CloudFront is a Content Delivery Service that delivers content, yes who could have put those two together, such as videos, pictures, or applications to users. CloudFront will cache content to AWS Edge locations, providing faster retrieval time for users after the first initial retrieval. CloudFront is a global service and provides access to the backbone of the AWS network so that content is more easily served globally. For more information click the link AWS CloudFront.


# What is S3:

Amazon S3 (Simple Storage Service) provides object storage, which is built for storing and recovering any amount of information or data from anywhere over the internet. It provides this storage through a web services interface. While designed for developers for easier web-scale computing, it provides 99.999999999 percent durability and 99.99 percent availability of objects. It can also store computer files up to 5 terabytes in size.

Apart from data storage functionality, the AWS S3 bucket provides a remarkable feature of static website hosting over it. A website that doesn’t involve server-side communication is called a static website.

# Purpose:
To provision, one S3 bucket with a Text script in it, and have CloudFront serve our content by using this bucket as the origin. CloudFront will use Edge Locations thus reducing latency for our users.

## Requirements:
- AWS account
- Experience with S3 
- Some Experience with CloudFront

# Let’s start:

## Creating & setting up S3 bucket:
Login into your AWS account, head over to the search bar at the top and search for S3.

![S3 search](/images/s3-cloudfront/s3%20search.png)


Inside of the S3 dashboard, click on “Create bucket”.

![Create bucket](/images/s3-cloudfront/2%20.create%20bucket.png)


Scroll to the bottom and click “Create bucket”.


![upload](/images/s3-cloudfront/1_UkFz-IRBRXZzgvcfSUQkng.jpeg)




Then edit the bucket policy like below image.


![Create bucket](/images/s3-cloudfront/bucket%20policy.png)



After creating the bucket, upload your website to the bucket by clicking on the bucket name. Once inside of your bucket on the “Objects” tab, click on the “Upload” button.


![upload](/images/s3-cloudfront/1_bYTwXcSGdFRwKi5o1UE33g.jpeg)




From here you can upload your files multiple ways. You can click “Add files”, “Add folder” or drag and drop your items. Once you’re done click “Upload”.

![Create bucket](/images/s3-cloudfront/1_XKQcRXCsjNrFKsgvjfNO3A.jpeg)



NB: Now go to the local code repository and run “npm run build” as it's js based project(React/Vue/Svelte)

![Create bucket](/images/s3-cloudfront/2.build.png)

And upload the files from ./dist directory.


![Create bucket](/images/s3-cloudfront/files%20upload.png)

The next step is to grant permissions to your bucket.

To do that, head over to the “Permissions” tab of your bucket. Scroll down to the “Bucket policy” section and click on the “Edit” button.


Paste the below code from below link into the bucket policy:  
https://github.com/tanvirewu/s3_bucket_policy/blob/master/bucket_policy


## Setting up cloudfront 

To Setup a CloudFront distribution go to “CloudFront” from the AWS console and follow these steps:

![Create bucket](/images/s3-cloudfront/create%20cloud.png)

Click “Create distribution” and choose  or enter your origin's domain name.Set the origin domain name to be the newly created s3 bucket.

Set the default root object to index.html so it redirects / to /index.html

![Create bucket](/images/s3-cloudfront/index.png)

Choose origin access and select Origin access control settings (recommended) and update the s3 bucket policy. 


![Create bucket](/images/s3-cloudfront/origin.png)

Click Create Distribution and wait until the distribution is created.



Now let’s create invalidation under the “invalidation” section. 

![Create bucket](/images/s3-cloudfront/invilidation.png)

Now,your website should be now accessible via the CloudFront distribution’s URL. 


![Create bucket](/images/s3-cloudfront/link.png)


And if everything is set up correctly, you should be able to see a webpage like this!

![Create bucket](/images/s3-cloudfront/cloudfront.png)




Thank you for reading. 

Regards

Tanvir Ahmed







