# Architecture — Tech Stack & Scaling Plan

## 1. Tech Stack

### Frontend

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Framework | Next.js 14 (React) | SSR for SEO-optional pages; App Router for clean layouts |
| UI Components | shadcn/ui + Tailwind CSS | Accessible, composable, no vendor lock-in |
| State Management | Zustand | Lightweight; avoids Redux boilerplate |
| Data Fetching | TanStack Query (React Query) | Optimistic updates; cache management |
| Email Composer | TipTap (rich text) | Inline AI suggestions; extensible |
| Spreadsheet | SheetJS (client-side) | Import/export without server round-trip for small files |

### Backend

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Runtime | Node.js 20 (TypeScript) | Shared types with frontend; large ecosystem |
| API framework | Fastify | Higher throughput than Express; TypeScript-first |
| ORM | Drizzle ORM | Type-safe SQL; migration tooling; no magic |
| Database | PostgreSQL 16 | Relational + JSONB; proven at scale |
| Job Queue | BullMQ (Redis) | Reliable async processing for email polling, AI calls |
| Auth | Better Auth (or Clerk) | RBAC; OAuth2 social login; session management |
| File Storage | AWS S3 (or Cloudflare R2) | Document uploads (contracts, quote sheets) |
| Secrets | AWS Secrets Manager | API keys, OAuth refresh tokens |

### AI / ML

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Primary LLM | OpenAI GPT-4o | Best-in-class for structured output + email drafting |
| Fallback LLM | Anthropic Claude 3.5 Sonnet | Redundancy; stronger reasoning in some contexts |
| Structured output | OpenAI JSON mode / function calling | Reliable JSON extraction from supplier emails |
| Embeddings | OpenAI text-embedding-3-small | Semantic search over past negotiation outcomes |
| Vector DB | pgvector (PostgreSQL extension) | Keeps stack simple; no additional service for v1 |

### Infrastructure

| Layer | Choice | Rationale |
|-------|--------|-----------|
| Hosting | AWS (ECS Fargate) | Serverless containers; auto-scaling; managed |
| CDN / Edge | CloudFront + S3 | Static assets and document delivery |
| DNS | AWS Route 53 | |
| CI/CD | GitHub Actions | PR checks, automated deploys to staging/prod |
| Container registry | Amazon ECR | |
| Monitoring | Datadog (or Grafana Cloud) | APM, logs, alerts |
| Error tracking | Sentry | Frontend and backend error capture |
| Alerting | PagerDuty | On-call escalation for P1 incidents |

---

## 2. Application Architecture

```
┌────────────────────────────────────────────────────────────────┐
│                        Client (Browser)                        │
│   Next.js App  ─  TanStack Query  ─  Zustand  ─  TipTap       │
└───────────────────────────┬────────────────────────────────────┘
                            │ HTTPS / REST + WebSocket
┌───────────────────────────▼────────────────────────────────────┐
│                      API Server (Fastify)                      │
│   Auth middleware  │  Rate limiter  │  Request validation      │
│                                                                │
│  Route handlers                                                │
│   ├── /negotiations  ── NegotiationService                     │
│   ├── /messages      ── MessageService  ── EmailProvider       │
│   ├── /suppliers     ── SupplierService                        │
│   ├── /projects      ── ProjectService                         │
│   └── /reports       ── ReportingService                       │
│                                                                │
│  AI Orchestration Layer                                        │
│   ├── ParseEmailAgent                                          │
│   ├── EvaluateQuoteAgent                                       │
│   └── DraftEmailAgent                                          │
└───────┬──────────────────────────────────────┬─────────────────┘
        │ SQL (Drizzle)                         │ BullMQ jobs
┌───────▼──────────┐                  ┌────────▼────────────────┐
│   PostgreSQL 16  │                  │   Redis (job queue)     │
│   + pgvector     │                  │                         │
└──────────────────┘                  └────────┬────────────────┘
                                               │
                                    ┌──────────▼──────────────────┐
                                    │   Worker Processes           │
                                    │   ├── EmailPollingWorker     │
                                    │   ├── AIInferenceWorker      │
                                    │   └── ReportGenerationWorker │
                                    └─────────────────────────────┘
```

---

## 3. Key Architectural Decisions

### Async AI Inference
AI calls (parsing, evaluation, drafting) are dispatched as BullMQ jobs rather than inline API calls. This prevents HTTP timeouts on slow LLM responses and allows retries with backoff on API errors. The frontend polls for job completion or receives a WebSocket push when ready.

### Email Integration Abstraction
All email send/receive logic is behind a `EmailProvider` interface. The concrete implementations (`GmailProvider`, `OutlookProvider`) are swappable without changing the business logic layer.

### JSONB for Flexible Data
`parsed_terms`, `trade_off_weights`, and `company_negotiation_policy` use PostgreSQL JSONB columns. This avoids premature schema rigidity while maintaining the benefits of a relational database for everything else.

### Single-Region v1, Multi-Region v2
v1 deploys to a single AWS region (us-east-1). Data residency requirements (e.g., EU customers) will drive multi-region deployment in v2 using Aurora Global Database or logical replication.

---

## 4. Scaling Plan

### v1 (0–1,000 users)
- Single ECS Fargate service (2 vCPU, 4 GB RAM), auto-scales to 4 instances.
- Single PostgreSQL RDS instance (db.t4g.medium), with automated backups.
- Redis ElastiCache (cache.t4g.micro) for BullMQ.
- Estimated cost: ~$200–400/month.

### v2 (1,000–10,000 users)
- API service scales horizontally behind an ALB; each instance stateless.
- Read replicas added to PostgreSQL for reporting queries.
- BullMQ worker pool scaled independently from API.
- AI inference costs managed via prompt caching and model-tier routing (GPT-4o-mini for parsing, GPT-4o for drafting).
- Estimated cost: ~$1,500–3,000/month.

### v3 (10,000+ users / Enterprise)
- Multi-region active/passive with Aurora Global Database.
- Dedicated AI inference tier with request batching and result caching.
- Tenant isolation: schema-per-tenant for large enterprise accounts.
- SOC 2 Type II audit initiated.
- Estimated cost: variable; priced per enterprise contract.

---

## 5. Security Considerations

| Area | Approach |
|------|----------|
| Authentication | JWT (short-lived access tokens) + refresh token rotation |
| Authorisation | Row-level security in PostgreSQL enforces company data isolation |
| Data at rest | PostgreSQL encrypted at rest (AWS RDS encryption); S3 SSE-S3 |
| Data in transit | TLS 1.3 everywhere; HSTS enforced |
| API keys | Stored in AWS Secrets Manager; never in code or env vars |
| Email content | Encrypted at rest in the database (`pgcrypto`) |
| OAuth tokens | Refresh tokens stored encrypted; access tokens never persisted |
| Audit logging | All data-modifying actions logged to an `audit_log` table |
| Penetration testing | Annual third-party pentest from v2 onwards |

---

## 6. Environments

| Environment | Branch | Purpose |
|------------|--------|---------|
| `local` | any | Developer machines; local PostgreSQL + Redis via Docker Compose |
| `staging` | `main` | Auto-deployed on every merge; mirrors production config |
| `production` | `release/*` | Manual promotion from staging; blue/green deployment |
