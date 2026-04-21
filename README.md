# 🏆 Golden Jackets Brazil

Community website celebrating Brazilian professionals who earned all active AWS certifications.

🔗 **[goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)**

## Structure

```
├── index.html              # Main website
├── assets/
│   ├── members/            # Member photos
│   ├── badges/             # AWS certification badges
│   ├── Designer.png        # Hero image
│   └── awstronaut*.jpg     # Additional assets
├── docs/
│   └── ARCHITECTURE.md     # AWS architecture diagram
└── .github/
    └── workflows/          # CI/CD (coming soon)
```

## Architecture

S3 Static Website → CloudFront (CDN + SSL) → WAF v2 (Bot Protection)

See [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) for full details.

## Deploy

Currently manual via AWS CLI. GitHub Actions CI/CD coming soon.

## Community

- **Website**: [goldenjacketsbrazil.com](https://goldenjacketsbrazil.com)
- **LinkedIn**: [Golden Jackets Brazil](https://lnkd.in/duqvaGdp)

---

*Independent community, not officially affiliated with Amazon Web Services.*
