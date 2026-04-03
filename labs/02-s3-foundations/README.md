# 02-s3-foundations

## Objective

Create, validate, secure, use, and clean up a basic Amazon S3 bucket using AWS CLI.

## Why this matters in real-world DevOps

S3 is a core AWS service used for object storage, logs, backups, static assets, artifacts, and many automation workflows. A DevOps engineer must know how to create a bucket with intention, validate it, protect it from accidental public exposure, and clean it up correctly.

## What S3 is

Amazon S3 is an object storage service.

Key concepts:
- **bucket**: the logical container
- **object**: the stored file
- **key**: the logical name/path of the object inside the bucket

S3 is not a normal Linux filesystem and it is not block storage.

## Scope

This lab covered:
- AWS CLI identity and region validation
- bucket naming with traceability
- bucket creation in `eu-west-1`
- bucket location validation
- public access block configuration
- bucket tagging
- object upload
- object listing
- object read validation
- full cleanup

## Prerequisites

- AWS account available
- MFA-enabled IAM user
- AWS CLI configured
- named profile: `pablog2-it`
- region selected: `eu-west-1`

## Bucket used in the lab

`pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1`

## Why the bucket name makes sense

The bucket name includes:
- user identifier
- project name
- sprint number
- lab purpose
- AWS account ID
- region hint

This improves uniqueness, traceability, and future cleanup.

## Commands used

```powershell
aws configure list-profiles
aws sts get-caller-identity --profile pablog2-it
aws configure list --profile pablog2-it

aws s3api create-bucket --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --region eu-west-1 --create-bucket-configuration LocationConstraint=eu-west-1 --profile pablog2-it

aws s3api head-bucket --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it
aws s3api get-bucket-location --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it

aws s3api put-public-access-block --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --public-access-block-configuration BlockPublicAcls=true,IgnorePublicAcls=true,BlockPublicPolicy=true,RestrictPublicBuckets=true --profile pablog2-it
aws s3api get-public-access-block --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it

aws s3api put-bucket-tagging --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --tagging 'TagSet=[{Key=Project,Value=DevOpsDublin2026},{Key=Sprint,Value=2},{Key=Env,Value=lab},{Key=Owner,Value=pablogs04},{Key=ManagedBy,Value=manual}]' --profile pablog2-it
aws s3api get-bucket-tagging --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it

Set-Content -Path .\s3-lab-note.txt -Value "Sprint 2 S3 lab validation file"
aws s3 cp .\s3-lab-note.txt s3://pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1/ --profile pablog2-it
aws s3 ls s3://pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1/ --profile pablog2-it
aws s3 cp s3://pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1/s3-lab-note.txt - --profile pablog2-it

aws s3 rm s3://pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1/s3-lab-note.txt --profile pablog2-it
aws s3 rb s3://pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it
aws s3api head-bucket --bucket pablogs04-devopsdublin2026-s2-s3lab-613098905611-euw1 --profile pablog2-it