# Security Policy

## Reporting Vulnerabilities

If you discover a security vulnerability in this project, please report it responsibly:

- **Email**: ricardo.gulias@darede.com.br
- **Do NOT** open a public GitHub issue for security vulnerabilities

## Security Measures

- HTTPS enforced via CloudFront
- WAF v2 with bot protection and rate limiting
- Cognito authentication with password policies
- CORS restricted to authorized domains
- Admin access restricted by email verification
- No static credentials in repository
- GitHub Actions uses OIDC federation for AWS access
- S3 versioning enabled for data recovery
- Automated backups (daily/weekly/monthly)

## Known Public Information

This is a public repository for a static website. The following are intentionally public:
- HTML source code (visible via browser inspector on any public website)
- AWS service architecture (documented for transparency)

The following are protected:
- User credentials and passwords (Cognito)
- API secrets and tokens (Lambda environment variables)
- Admin access (email-restricted)
- Backup data (AWS Backup vault)
