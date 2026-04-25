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
       ┌──────┴──────┐
       │  Lambda     │
       │  Admin API  │
       └─────────────┘

       ┌─────────────┐
       │ AWS Backup  │
       │ Daily/Weekly│
       │ Monthly     │
       └─────────────┘
```

## AWS Services

| Service | Purpose |
|---------|---------|
| **S3** | Static website hosting (2 buckets) |
| **CloudFront** | CDN, SSL termination, caching |
| **WAF v2** | Bot protection, rate limiting |
| **Route 53** | DNS management |
| **Cognito** | User authentication (Members Lounge) |
| **API Gateway** | HTTP API for member, article, sponsor, and admin endpoints |
| **Lambda** | Backend logic (applications, articles, sponsors, admin) |
| **SES** | Transactional emails |
| **SNS** | Admin notifications |
| **AWS Backup** | Automated S3 backups |
| **GitHub Actions** | CI/CD pipeline |

## Project Structure

```
├── index.html              # Main website
├── members.html            # Members Lounge (authenticated)
├── admin.html              # Admin Console (restricted)
├── card-generator.html     # Member card generator
├── assets/
│   ├── members/            # Member photos
│   ├── badges/             # AWS certification badges
│   ├── sponsors/           # Sponsor logos
│   └── *.png / *.jpg       # Site assets
├── .github/
│   └── workflows/
│       ├── deploy.yml      # S3 deploy + CloudFront invalidation
│       └── create-user.yml # User onboarding automation
└── README.md
```

## CI/CD

### Deploy (`deploy.yml`)
- Triggers on push to `main`
- Syncs to S3 buckets
- Invalidates CloudFront cache

### User Onboarding (`create-user.yml`)
- Triggers on PR merge (new members)
- Creates authenticated user
- Sends welcome email with 30min delay

## Backup Strategy

| Schedule | Retention |
|----------|-----------|
| Daily (5AM UTC) | 7 days |
| Weekly (Sunday) | 30 days |
| Monthly (1st) | 365 days |

## Security

- All traffic served over HTTPS via CloudFront
- WAF v2 with bot protection and rate limiting
- Cognito authentication for Members Lounge
- Admin Console restricted to authorized email
- CORS restricted to goldenjacketsbrazil.com domain
- S3 buckets with versioning enabled
- No secrets stored in repository
- GitHub Actions uses OIDC federation (no static credentials)

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| POST | `/apply` | Member application → GitHub PR |
| POST | `/article` | Article submission → GitHub PR |
| POST | `/sponsor` | Sponsor inquiry → notification + confirmation email |
| POST | `/admin` | Admin operations (authenticated) |

> API base URL, account IDs, and resource ARNs are not published for security. See internal documentation.

## Community

- **Website**: [goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)
- **LinkedIn**: [Golden Jackets Brazil](https://www.linkedin.com/company/golden-jackets-brazil)

## Contributing

Members can submit articles and content through the Members Lounge. For technical contributions, please open an issue or pull request.

## License

This project is maintained by the Golden Jackets Brazil community.

---

*Independent community, not officially affiliated with Amazon Web Services.*
