# 🏆 Golden Jackets Brazil

Community website celebrating Brazilian professionals who earned all active AWS certifications.

🔗 **[goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)**

## Architecture

```
                    ┌─────────────┐
                    │  CloudFront  │
                    │  (CDN + SSL) │
                    └──────┬──────┘
                           │
                    ┌──────┴──────┐
                    │   WAF v2    │
                    │(Bot Protect)│
                    └──────┬──────┘
                           │
              ┌────────────┼────────────┐
              │            │            │
       ┌──────┴──────┐ ┌──┴───┐ ┌──────┴──────┐
       │  S3 (www)   │ │  S3  │ │  S3 (origin)│
       │  Website    │ │Backup│ │  Website    │
       └─────────────┘ └──────┘ └─────────────┘

       ┌─────────────┐ ┌──────────────┐ ┌───────────┐
       │   Cognito    │ │ API Gateway  │ │  Route 53  │
       │  User Pool   │ │  (HTTP API)  │ │   (DNS)    │
       └──────┬──────┘ └──────┬───────┘ └───────────┘
              │               │
              │    ┌──────────┼──────────┐
              │    │          │          │
              │ ┌──┴───┐ ┌───┴──┐ ┌─────┴────┐
              │ │Lambda│ │Lambda│ │  Lambda   │
              │ │Apply │ │Article│ │ Sponsor  │
              │ └──┬───┘ └───┬──┘ └─────┬────┘
              │    │         │          │
              │    ▼         ▼          ▼
              │  GitHub    GitHub      SNS
              │   PR        PR      + SES
              │
       ┌──────┴──────┐ ┌──────────────┐
       │  Lambda     │ │  Lambda      │
       │  Admin API  │ │  gj-admin    │
       └─────────────┘ └──────────────┘

       ┌─────────────┐
       │ AWS Backup  │
       │ Daily/Weekly│
       │ Monthly     │
       └─────────────┘
```

## AWS Services Used

| Service | Purpose |
|---------|---------|
| **S3** | Static website hosting (2 buckets: www + origin) |
| **CloudFront** | CDN, SSL termination, caching |
| **WAF v2** | Bot protection, rate limiting |
| **Route 53** | DNS management |
| **Cognito** | User authentication (Members Lounge) |
| **API Gateway** | HTTP API for apply, article, sponsor, admin endpoints |
| **Lambda** | `gj-apply` (member applications), `gj-article` (article submissions), `gj-sponsor` (sponsor inquiries), `gj-admin` (admin operations) |
| **SES** | Transactional emails (sponsor confirmations, welcome emails) |
| **SNS** | Admin notifications (new applications, sponsor inquiries) |
| **AWS Backup** | Automated S3 backups (daily/weekly/monthly) |
| **GitHub Actions** | CI/CD (deploy to S3 + CloudFront invalidation + Cognito user creation) |

## Structure

```
├── index.html              # Main website (Golden Jackets + Challengers + Articles + Sponsors)
├── members.html            # Members Lounge (authenticated area)
├── admin.html              # Admin Console (restricted to founder)
├── card-generator.html     # Member card generator tool
├── assets/
│   ├── members/            # Member photos
│   ├── badges/             # AWS certification badges
│   ├── sponsors/           # Sponsor logos
│   ├── Designer.png        # Hero logo
│   └── geriesabouayash.jpg # Geries quote photo
├── .github/
│   └── workflows/
│       ├── deploy.yml      # S3 sync + CloudFront invalidation
│       └── create-user.yml # Cognito user creation + welcome email
└── README.md
```

## API Endpoints

Base URL: `https://kqiq2bltjd.execute-api.us-east-1.amazonaws.com`

| Method | Path | Lambda | Description |
|--------|------|--------|-------------|
| POST | `/apply` | gj-apply | Member application → creates GitHub PR |
| POST | `/article` | gj-article | Article submission → creates GitHub PR |
| POST | `/sponsor` | gj-sponsor | Sponsor inquiry → SNS + SES confirmation |
| POST | `/admin` | gj-admin | Admin operations (list users, create, delete, resend, backup) |

## AWS Backup

| Schedule | Retention | Vault |
|----------|-----------|-------|
| Daily (5AM UTC) | 7 days | gj-site-backups |
| Weekly (Sunday 5AM UTC) | 30 days | gj-site-backups |
| Monthly (1st, 5AM UTC) | 365 days | gj-site-backups |

## GitHub Actions Workflows

### Deploy to S3 (`deploy.yml`)
- Triggers on push to `main`
- Syncs files to both S3 buckets
- Invalidates CloudFront cache

### Create Cognito User (`create-user.yml`)
- Triggers on PR merge with title "New Member:"
- Creates Cognito user with temporary password
- Sends welcome email via SES (30min delay)

## AWS Accounts

| Account | ID | Purpose |
|---------|-----|---------|
| Golden Jackets | 800712212925 | Cognito, API Gateway, Lambda, Backup, WAF, CloudFront, S3 (www) |
| Origin | 948949707127 | S3 (origin bucket) |

## Cognito User Pool

- **Pool ID**: `us-east-1_Z0VzzrmIX`
- **Client ID**: `6p0utci3h0mfsv02k4848vhhch`
- **Region**: us-east-1
- **Auth flow**: USER_PASSWORD_AUTH

## SNS Topic

- **ARN**: `arn:aws:sns:us-east-1:800712212925:goldenjackets-alerts`
- Sends notifications for new member applications and sponsor inquiries

## Community

- **Website**: [goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)
- **LinkedIn**: [Golden Jackets Brazil](https://www.linkedin.com/company/golden-jackets-brazil)
- **Discord**: [Join Server](https://discord.gg/qntq7b7UqF)

## Founder

Ricardo Gulias — AWS Golden Jacket, 12x AWS Certified
📱 WhatsApp: +55 11 93248-9800

---

*Independent community, not officially affiliated with Amazon Web Services.*
