# CloudFront Setup for S3 Hosted Website
## Steps:
1. Configure S3 bucket for static website hosting.
2. Enable public access with bucket policy.
3. Create a CloudFront distribution.
4. Customize cache settings.
5. [Optional] Use a custom domain via Route 53.

## Useful Commands:
1.Create and configure S3 bucket for static website hosting:
-------------------------------------------------------------

   aws s3 mb s3://<your-bucket-name>
   aws s3 website s3://<your-bucket-name>/ --index-document index.html --error-document error.html

2.Enable public access on the S3 bucket with a policy:
-------------------------------------------------------

   aws s3api put-bucket-policy --bucket <your-bucket-name> --policy file://s3-bucket-policy.json

3.Upload website files to S3 bucket:
------------------------------------

   aws s3 cp /path/to/your/index.html s3://<your-bucket-name>/index.html
   aws s3 cp /path/to/your/error.html s3://<your-bucket-name>/error.html

4.Create CloudFront Distribution:
----------------------------------

   aws cloudfront create-distribution --origin-domain-name <your-bucket-name>.s3.amazonaws.com --default-root-object index.html

5.Update CloudFront Cache Settings:
-----------------------------------

   aws cloudfront update-distribution --id <distribution-id> --default-cache-behavior '{"MinTTL": 60, "DefaultTTL": 300, "MaxTTL": 3600}'

6.Update DNS with Custom Domain in Route 53 (Optional):
--------------------------------------------------------

   aws route53 change-resource-record-sets --hosted-zone-id <hosted-zone-id> --change-batch '{
      "Changes": [{
         "Action": "UPSERT",
         "ResourceRecordSet": {
               "Name": "<your-custom-domain>.com",
               "Type": "CNAME",
               "TTL": 60,
               "ResourceRecords": [{
                  "Value": "<your-cloudfront-distribution>.cloudfront.net"
               }]
         }
      }]
   }'

