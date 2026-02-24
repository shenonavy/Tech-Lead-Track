# Technology Roadmap: 2025–2028



## Strategic Objectives

1. Enable international expansion to 5 markets  
2. Launch B2B wholesale platform  
3. Scale platform to 10M MAU  
4. Improve engineering velocity and reduce operational risk  

---

# Roadmap Overview

This roadmap follows an **evolutionary modernization strategy** aligned with business growth goals, budget constraints ($2M/year), and limited hiring capacity (10 engineers/year).

**2025:** Architectural foundation and multi-region readiness  
**2026:** B2B launch and scalability improvements  
**2027–2028:** Optimization, automation, and global acceleration  

---

# Phase 1: Foundation (Q1–Q2 2025)

**Theme:** Decouple and Prepare  
**Goal:** Enable modularization and future service extraction without rewriting.

| Initiative | Dependencies | Team Size | Investment |
|------------|--------------|-----------|------------|
| API Gateway Introduction | None | 3 | $200K |
| Identity/Auth Service Extraction | API Gateway | 2 | $150K |
| CI/CD Modernization + Infrastructure-as-Code | None | 3 | $250K |
| Observability Platform (Logs + Metrics + Tracing) | CI/CD | 2 | $150K |

**Total Investment:** ~$750K  

### Key Deliverables

- API Gateway handling 100% of external traffic  
- Identity service deployed independently  
- Infrastructure provisioned via IaC  
- Centralized logging, metrics, and distributed tracing  

### Exit Criteria

- [ ] API Gateway routing all traffic  
- [ ] Auth service deployed  
- [ ] 80% infrastructure managed as code  
- [ ] Deployment frequency doubled  

### Business Impact

- Reduced deployment risk  
- Improved security posture  
- Platform ready for domain extraction  
- Faster feature delivery  

---

# Phase 2: Expansion Ready (Q3–Q4 2025)

**Theme:** Multi-Region Foundation  
**Goal:** Enable entry into first 2 international markets.

| Initiative | Dependencies | Team Size | Investment |
|------------|--------------|-----------|------------|
| Regional Infrastructure Setup (2 regions) | IaC | 4 | $400K |
| Regional Database Strategy (Data Isolation) | Infra setup | 3 | $300K |
| Payment Provider Internationalization | API Gateway | 2 | $150K |
| Compliance Framework (GDPR + Data Lifecycle Controls) | Regional DB | 2 | $150K |

**Total Investment:** ~$1M  

### Key Deliverables

- Active-active regional clusters  
- Regional database isolation  
- GDPR-compliant data lifecycle management  
- Multi-currency and localized payments  

### Exit Criteria

- [ ] Region A and B live  
- [ ] Data residency controls validated  
- [ ] Cross-region failover tested  
- [ ] First international market launched  

### Business Impact

- Revenue growth from new markets  
- Reduced regulatory exposure  
- Improved platform resilience  

---

# Phase 3: B2B Launch (Q1–Q2 2026)

**Theme:** New Business Line  
**Goal:** Deliver B2B wholesale platform leveraging shared commerce core.

| Initiative | Dependencies | Team Size | Investment |
|------------|--------------|-----------|------------|
| B2B Account Service | Identity Service | 3 | $250K |
| Pricing & Bulk Discount Engine | Catalog modularization | 3 | $250K |
| Invoice & Net Terms Module | Payments integration | 2 | $150K |
| Admin & Organization Management Portal | B2B Account Service | 2 | $150K |

**Total Investment:** ~$800K  

### Key Deliverables

- Organization-based accounts  
- Tiered pricing and bulk ordering  
- Net payment terms and invoicing  
- Dedicated B2B admin controls  

### Exit Criteria

- [ ] B2B pilot customers onboarded  
- [ ] B2B GMV tracked separately  
- [ ] <2% production defect rate at launch  

### Business Impact

- New revenue stream  
- Higher average order value  
- Increased enterprise customer retention  

---

# Phase 4: Scale (Q3–Q4 2026)

**Theme:** Performance and Growth  
**Goal:** Scale platform from 5M to 10M MAU.

| Initiative | Dependencies | Team Size | Investment |
|------------|--------------|-----------|------------|
| Event Bus Implementation | Service modularization | 3 | $250K |
| Order & Catalog Service Extraction | Modular monolith | 4 | $400K |
| Caching & Performance Optimization | Observability | 2 | $150K |
| Data Warehouse & Advanced Analytics | Event Bus | 2 | $200K |

**Total Investment:** ~$1M  

### Key Deliverables

- Event-driven architecture for core flows  
- Independently scalable catalog and order services  
- Reduced database bottlenecks  
- Real-time business analytics  

### Exit Criteria

- [ ] Platform load tested for 10M MAU  
- [ ] P95 latency < 300ms  
- [ ] 99.95% availability achieved  
- [ ] Zero Sev-1 incidents during peak events  

### Business Impact

- Supports 4x revenue growth  
- Improved system reliability  
- Data-driven decision making  

---

# Dependencies and Risks

| Risk | Probability | Impact | Mitigation |
|------|------------|--------|------------|
| Over-ambitious service extraction | Medium | High | Modular monolith first |
| Budget overrun | Medium | High | Quarterly financial reviews |
| Hiring delays | High | Medium | Automation-first delivery |
| Multi-region latency issues | Medium | High | Early load testing |
| Regulatory misinterpretation | Low | High | Legal and compliance audits |

---

# Resource Plan

## Team Structure Evolution

### 2025 (25 → 35 Engineers)

- Platform Team (Infrastructure + DevOps) – 6  
- Commerce Core Team – 8  
- Customer Experience Team – 6  
- New Services Team – 5  
- Data/Analytics – 2  
- QA/Automation – 3  
- Security – 1  

### 2026 (35 → 45 Engineers)

- Dedicated B2B Team – 6  
- Regional Platform Squad – 5  
- Site Reliability Engineering (SRE) – 4  

Transition toward domain-aligned squads.

---

## Skills Requirements

- Cloud-native architecture  
- Infrastructure-as-Code  
- Distributed systems design  
- Data privacy & compliance  
- Event-driven architecture  
- Performance engineering  

---

## Hiring Plan

### Year 1 (10 hires)

- 3 Platform Engineers  
- 3 Backend Engineers  
- 2 QA Automation Engineers  
- 1 Security Engineer  
- 1 Data Engineer  

### Year 2 (10 hires)

- 4 Backend Engineers (B2B focus)  
- 2 SRE Engineers  
- 2 Data Engineers  
- 2 Frontend Engineers  

Focus on senior, high-leverage hires.

---

# Success Metrics

| Milestone | Metric | Target |
|-----------|--------|--------|
| Phase 1 Complete | Deployment frequency | 2x current |
| Phase 2 Complete | Time to launch new region | < 4 months |
| Phase 3 Complete | B2B revenue contribution | 15% of total revenue |
| Phase 4 Complete | Monthly Active Users | 10M |
| End 2026 | Availability | 99.95% |
| Ongoing | Lead time for change | < 2 days |
| Ongoing | Change failure rate | < 10% |

---

# Financial Alignment

Annual technology investment remains within the $2M/year constraint:

- ~40% modernization and infrastructure  
- ~30% new capabilities (B2B)  
- ~20% scaling and performance  
- ~10% compliance and security  

This roadmap:

- Avoids high-risk system rewrite  
- Delivers revenue-generating B2B capabilities by 2026  
- Enables international expansion within 12–18 months  
- Supports 4x user growth without proportional cost growth  