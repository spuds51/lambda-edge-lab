# Dev Labs : A/B testing with lambda@edge

Instructions for setting up the lab

## Pre-requisites

1. AWS CLI
2. SAM CLI
3. GNU Make

```bash
./install_prereqs.sh
```

## Set Up:

```bash
make setup
```

Deploys a CloudFormation stack containing:

  -   A CloudFront distribution with:
      -   A 'dummy' or default S3 origin bucket
      -   An S3 bucket for collecting CloudFront access logs
      -   A CloudFront Origin Access Identity for authenticating requests from the cloudfront distribution to the S3 origin buckets
      -   2 x node10.x Lambda@edge functions:
          -   OriginRequest - associated with the distribution's origin-request event 
          -   OriginResponse - associated with the distribution's origin-response event

The stack is annotated with tags: `purpose=lab` and `product=lambda-edge-ab`

## Reset

```bash
make reset
```

This will:
1. delete the content from the S3 origin buckets
2. delete the custom S3 bucket origins
3. create a cache invalidation request to invalidate the cach of the cloudfront distribution