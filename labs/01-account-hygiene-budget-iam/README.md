@'
# 01-account-hygiene-budget-iam

## Objective

Establish a clean and secure AWS account baseline for Sprint 2.

## Why this matters in real-world DevOps

Before provisioning cloud resources, engineers must verify account context, separate identities, enable MFA, and put cost awareness controls in place. This reduces operational mistakes, security risk, and unnecessary spend.

## Scope

This lab covers:

- root account hygiene review
- MFA validation
- admin and daily user separation
- AWS CLI profile validation
- early budget awareness
- initial tagging convention

## What was done

- Verified the active AWS account and caller identity
- Confirmed the root user has MFA enabled
- Confirmed the root user has no active access keys
- Reviewed the existing administrative IAM user
- Enabled MFA for `pabloadmin`
- Created a daily operator user: `pablog2-it`
- Created a temporary bootstrap admin group
- Added `pablog2-it` to the bootstrap group
- Created and validated a named AWS CLI profile for `pablog2-it`
- Deactivated the old access key for `pabloadmin`
- Reviewed existing budget alerts and kept them as early warning controls

## Validation

The lab was validated by confirming:

- the correct AWS account ID
- successful console login with MFA
- a working AWS CLI named profile
- `aws sts get-caller-identity --profile pablog2-it`
- the expected ARN for `pablog2-it`
- the old `pabloadmin` access key was set to inactive

## Common mistakes

- Working in the wrong AWS account
- Using the root user for daily work
- Reusing stale credentials
- Leaving old access keys active
- Assuming budgets automatically stop spend

## Security note

- Root user is reserved for exceptional tasks only
- MFA is enabled on human identities
- Daily work is separated from break-glass administration
- No secrets are committed to Git
- Old credentials are being retired in a controlled way

## Cost note

- Existing budget alerts remain enabled as early warning controls
- Resources must be reviewed and cleaned up at the end of each session
- Small and low-cost services should be preferred during the sprint

## Cleanup

No infrastructure resources were created in this lab.
Identity and account hygiene changes were reviewed and validated.

## Evidence

Store sanitized screenshots and non-sensitive command outputs in:
- `evidence/`
- `notes/`
- `artifacts/`

## Lessons learned

- Always verify account identity before creating resources
- Root MFA does not replace IAM user MFA
- A named AWS CLI profile is safer than relying on `default`
- Budget alerts help, but cleanup discipline is still mandatory