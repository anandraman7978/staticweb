Deployment of a  Static Website

Details the approach followed to host a static website using AWS S3,Cloudfront and IAM Policies.


Install Steps:

1. Our site will be hosted on S3 and served via CloudFront CDN. You will need external access to your AWS resources so it's best to setup a new IAM user with AmazonS3FullAccess and CloudFrontFullAccess policy only.
2. Hosting on S3:
	1. Go to S3 in your AWS account.
	2. Create a new bucket on S3
	3. By default your bucket is private and no one can access it so we have to configure it to make it publicly available:
	   Open the properties tab, click on Static Website Hosting and check Enable Website Hosting. Also fill in the path to your index and error page (you can do this later after setting up you repo).
			You also have to give read access to public otherwise no one could access the bucket although static hosting is enabled. To set the access click on Permissions and Edit bucket policy and fill in the following policy but replace YOUR_BUCKET_NAME with - you wouldn't have guessed it - your bucket name
				{
					"Version": "2012-10-17",
					"Id": "Policy1478014846282",
					"Statement": [
						{
							"Sid": "Stmt1478014844834",
							"Effect": "Allow",
							"Principal": "*",
							"Action": "s3:GetObject",
							"Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
						}
					]
				}
3. CloudFront as CDN
	1. Go to CloudFront in your AWS account
	2. Create a new Web distribution
	3. Configure your distribution:
	4. Set your bucket as Origin domain name. This will link CloudFront and S3
	5. Set the index.html file as Default Root Object. This will allow the user to access your domain without any path and still get the index file.
	6. Click on Create Distribution to create your CloudFront CDN


Usage:
http://udacity-project-7978.s3-website.ca-central-1.amazonaws.com/


License
Licensed under the [MIT License](LICENSE).