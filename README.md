# Static Web Hosting with AWS S3, CloudFront, CodePipeline, and Git

This project demonstrates the deployment of a static website to AWS S3 using AWS CloudFront for content delivery, and AWS CodePipeline to automate the deployment process from a Git repository. Whenever code is updated in the connected Git repository, it will automatically trigger a pipeline that deploys the updated site to S3 and reflects the changes on the website.

## Architecture Overview

1. S3 : Static website hosting.
2. CloudFront : Content delivery network (CDN) to serve the website with low latency.
3. CodePipeline : Continuous integration and delivery (CI/CD) pipeline to automate the deployment process.
4. Git : Code repository (e.g., GitHub) that stores the website's source code.

## Project Setup

### Step 1: Set up S3 for Static Website Hosting

1. Go to the AWS Management Console.
2. Navigate to **S3** and create a new bucket for hosting the static site (e.g., `static-web hosting-project`).
   
   ![Screenshot (26)](https://github.com/user-attachments/assets/13f5aa83-128d-4160-aa9d-6b8463c72be2)

4. In the bucket properties, enable **Static Website Hosting**.

   ![Screenshot (28)](https://github.com/user-attachments/assets/89fdda16-0317-44d4-a7bd-264da788c21e)

6. Configure the index and error document names (e.g., `index.html` and `error.html`).
7. Set up bucket policy to allow cloudfront access to the files in the bucket.

   ![Screenshot (30)](https://github.com/user-attachments/assets/b4f10dbb-5226-4288-a844-8c9e98914905)


### Step 2: Set up CloudFront Distribution

1. Go to **CloudFront** in the AWS console.
2. Create a new CloudFront distribution.
3. In the origin settings, select the S3 bucket created in step 1 as the origin.
4. Set the default root object to `index.html`.
5. Wait for the CloudFront distribution to be deployed.

   ![Screenshot (31)](https://github.com/user-attachments/assets/de7dc8c8-3d30-44a7-94ae-8b95c6fe3f9c)


### Step 3: Set up CodePipeline for CI/CD

1. Go to **CodePipeline** in the AWS console.

   ![Screenshot (33)](https://github.com/user-attachments/assets/9e634d6a-9bf9-4673-b9c3-e835bad184ad)

3. Create a new pipeline with the following stages:
   - **Source**: Connect to your Git repository (GitHub, Bitbucket, or AWS CodeCommit).
  
   ![Screenshot (35)](https://github.com/user-attachments/assets/4cb265b1-6271-43aa-bd57-3400cf9c0867)

   - **Deploy**: Set up a deployment action to upload the files to the S3 bucket.
4. Configure triggers to automatically start the pipeline whenever there is a change in the Git repository.

### Step 4: Commit Changes

1. Push changes to your Git repository.

   ![Screenshot (37)](https://github.com/user-attachments/assets/21215659-aa26-42ce-8471-d92513e4dcb9)

3. CodePipeline will automatically trigger and deploy the updated website to the S3 bucket.
4. CloudFront will update the cached content, and the website will reflect the latest changes.


**CodePipeline will automatically detect the changes** and deploy them to S3. Once CloudFront has propagated the update, your changes will be live on the website.



