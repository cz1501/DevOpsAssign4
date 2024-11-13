Project Documentation: Static Website Deployment on AWS
1. Overview
This documentation describes the architecture, setup, and maintenance for a CI/CD pipeline that automates the deployment of a static website on Amazon S3. This website hosts your resume, and AWS services ensure smooth deployment and maintenance.

2. Architecture Overview
Components Used:
Amazon S3: Hosts the static website.
AWS CodePipeline: Provides continuous integration and deployment capabilities.
GitHub: Source control repository for the website code.
Workflow:
Code is pushed to the main branch of the GitHub repository.
AWS CodePipeline detects the code change and triggers the pipeline.
CodePipeline deploys the website to S3.
S3 serves the website publicly as a static site.

3. Configuration
3.1 Amazon S3
Bucket Setup:

Create an S3 bucket (e.g., my-resume-website) and enable it for static website hosting.
Configure the bucket permissions and bucket policy to allow public access.
Set up the index document (e.g., index.html) in the static website hosting settings.
Bucket Policy for Public Access:

Set up a policy allowing s3:GetObject access to all objects in the bucket.
json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::your-bucket-name/*"
    }
  ]
}
3.2 AWS CodePipeline
Pipeline Creation:

Set up a new pipeline with a source, build (optional), and deploy stage.
Source Stage:

Source provider: GitHub.
Branch: Specify the branch that CodePipeline should monitor, such as main.
Build Stage (Optional):

If the website code needs to be built or processed (e.g., minified, optimized), use CodeBuild.
Define a buildspec.yml file for CodeBuild with steps to install dependencies and build the code.
Deploy Stage:

Deploy provider: Amazon S3.
Bucket: Specify the S3 bucket for the website.
Enable overwriting to update files on each deployment.

4. Maintenance and Troubleshooting
Pipeline Management:

Monitor pipeline execution logs in the CodePipeline console.

Bucket Management:

Periodically review the S3 bucket policy and access settings for security.
Clear outdated or unused files to optimize storage.
