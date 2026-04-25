# 🏆 Golden Jackets Brazil — Backlog

## ✅ Concluído

### Infraestrutura
- [x] Site estático S3 + CloudFront + WAF
- [x] Cognito User Pool (autenticação Lounge)
- [x] API Gateway HTTP API (apply, article, sponsor, admin)
- [x] Lambdas: gj-apply, gj-article, gj-sponsor, gj-admin
- [x] SES para emails transacionais
- [x] SNS para notificações admin
- [x] AWS Backup (diário/semanal/mensal)
- [x] GitHub Actions CI/CD (deploy + user onboarding)
- [x] Smoke tests no pipeline
- [x] CloudWatch alarmes nas Lambdas
- [x] Cognito JWT Authorizer no /admin
- [x] GitHub Secrets (sem IDs hardcoded)
- [x] SECURITY.md + README atualizado

### Site
- [x] Seção Golden Jackets com cards numerados
- [x] Seção Challengers (cards prata)
- [x] Seção Articles & Talks com tags (Article/Talk)
- [x] Seção Sponsors com formulário
- [x] Seção Events com countdown
- [x] Mapa interativo com pins dourados/prata
- [x] Filtro por estado (Golden + Challengers)
- [x] Medalhas automáticas (🥇🥈🥉) para top contributors
- [x] Contadores dinâmicos (JS conta cards)
- [x] Tagline do Geries no hero
- [x] Missão destacada no About
- [x] Tags coloridas (Awstronaut, Speaker, Ambassador)
- [x] Badges de certificação em pirâmide

### Lounge
- [x] Autenticação Cognito
- [x] Change Password (1st Login)
- [x] Forgot Password
- [x] Enter key no login
- [x] Submit Article
- [x] Discord link
- [x] Admin Console (página separada)

### Admin Console
- [x] List Users (via API)
- [x] Create User (formulário)
- [x] Delete User
- [x] Resend Pending
- [x] Backup Status
- [x] Restore
- [x] Links GitHub (PRs, Actions)
- [x] Card Generator
- [x] Protegido por JWT

---

## 🔴 Alta Prioridade

### Segurança
- [ ] SES sair do sandbox (solicitado, aguardando AWS)
- [ ] Rate limiting no API Gateway (prevenir abuse nos forms públicos)
- [ ] Validação de input nas Lambdas (sanitizar nome, email, URL)

### Bugs Conhecidos
- [ ] Lambda gj-apply: marker frágil — qualquer mudança no layout pode quebrar inserção de cards
- [ ] Lambda gj-article: mesmo problema de marker
- [ ] Contadores hardcoded nas Lambdas (deveria usar contadores dinâmicos do JS e não mexer)

---

## 🟡 Média Prioridade

### Refatoração (fazer com cuidado, branch separada)
- [ ] Separar CSS em arquivo externo (styles.css)
- [ ] Separar JS em arquivo externo (app.js)
- [ ] CSS inline → classes reutilizáveis
- [ ] Minificação HTML/CSS/JS no pipeline

### Funcionalidades
- [ ] Email de boas-vindas automático (aguardando SES produção)
- [ ] Seção Challengers: formulário de aplicação específico (11/12)
- [ ] Promover Challenger → Golden Jacket (botão no admin)
- [ ] Dashboard de métricas no admin (membros/mês, artigos/mês)
- [ ] Exportar lista de membros (CSV) no admin
- [ ] Notificação no Discord quando novo membro entra

### Comunidade
- [ ] Talk no Community Day Brasília (27/06) — submissão feita
- [ ] Buscar patrocinadores (media kit pronto)
- [ ] Newsletter mensal para membros
- [ ] Página de eventos passados (galeria de fotos)

---

## 🟢 Baixa Prioridade / Futuro

### Técnico
- [ ] Migrar Lambdas para IaC (CDK ou SAM)
- [ ] Testes unitários nas Lambdas
- [ ] EventBridge: lembrete automático para pendentes (a cada 24h)
- [ ] Cognito custom domain (auth.goldenjacketsbrazil.com)
- [ ] SES custom domain (noreply@goldenjacketsbrazil.com)
- [ ] Monitoramento de custos (Budget alarm)

### Site
- [ ] Dark/Light mode persistente (salvar preferência)
- [ ] Página individual por membro (perfil completo)
- [ ] Seção de vídeos/talks (quando tiver conteúdo)
- [ ] Blog integrado (posts longos)
- [ ] Internacionalização completa (PT/EN toggle)
- [ ] PWA (Progressive Web App) — acesso offline
- [ ] SEO: sitemap.xml, robots.txt, meta tags por página

### Comunidade
- [ ] Programa de mentoria (Golden Jackets → Challengers)
- [ ] Ranking de contribuições (artigos, talks, mentoria)
- [ ] Certificação interna da comunidade
- [ ] Meetups regionais (SP, RJ, PR)
- [ ] Parceria com AWS User Groups
- [ ] Submeter para AWS Community Builder / Hero

---

*Última atualização: 25/04/2026*
