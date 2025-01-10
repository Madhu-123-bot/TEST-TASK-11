# CloudFront Setup for S3 Hosted Website
## Steps:
1. Configure S3 bucket for static website hosting.
2. Enable public access with bucket policy.
3. Create a CloudFront distribution.
4. Customize cache settings.
5. [Optional] Use a custom domain via Route 53.

## Useful Commands:
- Configure S3 website hosting:
  ```
  aws s3 website s3://<your-bucket-name>/ --index-document index.html --error-document error.html
  ```
- Create CloudFront Distribution:
  ```
  aws cloudfront create-distribution --origin-domain-name <your-bucket-name>.s3.amazonaws.com --default-root-object index.html
  ```
- Update CloudFront Cache Settings:
  ```
  aws cloudfront update-distribution --id <distribution-id> --default-cache-behavior '{"MinTTL": 60, "DefaultTTL": 300, "MaxTTL": 3600}'
  ```
