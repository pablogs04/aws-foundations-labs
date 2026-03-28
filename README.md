@'
# aws-foundations-labs

Sprint 2 of the **DevOps Dublin 2026** project.

This repository contains my hands-on AWS foundations labs focused on:

- AWS account hygiene
- cost awareness and cleanup
- IAM and least privilege basics
- AWS CLI profiles
- S3 fundamentals
- EC2 fundamentals
- CloudWatch basics
- foundational networking concepts
- security-minded documentation and operational validation

## Repository goals

- Learn AWS foundations through reproducible labs
- Build interview-defensible cloud experience
- Document security, validation, cleanup, and common mistakes
- Avoid hardcoded secrets and unsafe defaults

## Repository structure

- `docs/` -> glossary, checklist, cross-lab notes
- `labs/` -> hands-on labs with evidence
- `templates/` -> reusable lab templates

## Security and cost policy

- No secrets committed to Git
- No hardcoded credentials
- MFA-enabled human access
- Cleanup at the end of each session
- Small, low-cost resources only unless explicitly justified
- Tag resources consistently

## Initial tagging convention

- `Project=DevOpsDublin2026`
- `Sprint=2`
- `Env=lab`
- `Owner=pablogs04`
- `ManagedBy=manual`

## Current labs

- `01-account-hygiene-budget-iam` - in progress
