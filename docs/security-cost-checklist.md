# security-cost-checklist

## Security checklist

- Use the correct AWS account before making changes
- Do not use the root user for daily operations
- Enable MFA on human users
- Prefer named AWS CLI profiles over `default`
- Do not commit secrets, keys, or credentials to Git
- Review active access keys and retire old ones
- Keep administrative access separated from daily work
- Sanitize screenshots and command outputs before publishing

## Cost checklist

- Review budget alerts before starting new labs
- Prefer small, low-cost resources by default
- Tag resources consistently
- Validate quickly and avoid idle resources
- Stop or remove resources at the end of the session
- Re-check for leftover instances, volumes, IPs, and snapshots
- Document cleanup steps in every lab
- Treat budget alerts as warning signals, not hard stops

## End-of-session cleanup reminder

- Check running resources
- Confirm no unintended storage is left behind
- Verify no unused public exposure remains
- Update the lab README with validation and cleanup notes