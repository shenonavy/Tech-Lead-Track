# Build vs Buy Analysis

This document evaluates three strategic components required to support international expansion, B2B launch, and platform scalability:

1. Payment Processing
2. Multi-Region Database Strategy
3. B2B Commerce Engine

Each component is evaluated using weighted decision criteria aligned to business goals: speed, cost efficiency, scalability, compliance, and strategic differentiation.

---

# Component 1: Payment Processing

## Context

International expansion requires:

- Multi-currency support
- Local payment methods
- Regulatory compliance (PSD2, SCA, etc.)
- Fraud detection
- High availability

The current system integrates directly with a single regional payment provider.

---

## Options

1. **Build:** Custom payment gateway and orchestration layer
2. **Buy:** Stripe, Adyen, or similar global PSP
3. **Hybrid:** Buy PSP + build internal orchestration abstraction

---

## Evaluation Matrix

| Criterion | Weight | Build | Buy | Hybrid |
|------------|--------|--------|------|---------|
| Time to Market | 20% | 1/5 | 5/5 | 4/5 |
| 3-Year Total Cost | 25% | 2/5 | 4/5 | 3/5 |
| Global Coverage | 15% | 2/5 | 5/5 | 5/5 |
| Flexibility | 15% | 5/5 | 3/5 | 4/5 |
| Maintenance Burden | 15% | 1/5 | 5/5 | 3/5 |
| Strategic Differentiation | 10% | 3/5 | 2/5 | 4/5 |
| **Weighted Score** |  | **2.05** | **4.25** | **3.95** |

---

## Recommendation

**Buy (Stripe or Adyen) with light internal abstraction layer**

---

## Rationale

- Fastest path to international markets
- Built-in compliance (SCA, fraud detection)
- Reduces operational burden
- Avoids regulatory risk
- Keeps team focused on revenue-generating capabilities

Payments are not a strategic differentiator; commerce experience is.

---

## Implementation Plan

1. Introduce Payment Service abstraction behind API Gateway
2. Integrate global PSP
3. Support multi-currency and localized methods
4. Implement monitoring + failover strategy
5. Phase out direct monolith integration

**Timeline:** Q2–Q3 2025  
**Investment:** ~$50K–$80K/year (vendor + integration effort)

---

# Component 2: Multi-Region Database Strategy

## Context

Business requirements:

- Data residency (GDPR compliance)
- High availability
- 10M MAU scalability
- Reduced DB bottleneck risk

Current state: single-region RDBMS with shared schema.

---

## Options

1. **Build:** Custom sharded database architecture
2. **Buy:** Managed global distributed DB (e.g., Aurora Global, Spanner, Cosmos DB)
3. **Hybrid:** Regional managed DBs + application-level data partitioning

---

## Evaluation Matrix

| Criterion | Weight | Build | Buy | Hybrid |
|------------|--------|--------|------|---------|
| Time to Market | 20% | 2/5 | 4/5 | 4/5 |
| Compliance Fit | 20% | 3/5 | 4/5 | 5/5 |
| Scalability | 20% | 5/5 | 5/5 | 4/5 |
| Operational Complexity | 15% | 1/5 | 5/5 | 3/5 |
| Cost (3-Year) | 15% | 2/5 | 3/5 | 4/5 |
| Flexibility | 10% | 5/5 | 3/5 | 4/5 |
| **Weighted Score** |  | **2.65** | **4.15** | **4.25** |

---

## Recommendation

**Hybrid: Regional managed databases per market with logical partitioning**

---

## Rationale

- Enables strict data residency
- Avoids global write latency
- Balances operational simplicity with flexibility
- Avoids vendor lock-in from highly proprietary distributed DBs
- Lower risk than custom sharding

Each region operates its own primary database cluster.

---

## Implementation Plan

1. Define data residency boundaries
2. Deploy managed DB per region
3. Refactor services to enforce regional isolation
4. Introduce replication for analytics only
5. Implement disaster recovery strategy

**Timeline:** Q3–Q4 2025  
**Investment:** ~$300K (infra + migration effort)

---

# Component 3: B2B Commerce Engine

## Context

B2B requires:

- Organization accounts
- Tiered pricing
- Bulk ordering
- Net payment terms
- Approval workflows
- Dedicated admin management

Current monolith only supports B2C workflows.

---

## Options

1. **Build:** Extend modular monolith and extract B2B domain services
2. **Buy:** SaaS B2B commerce platform (e.g., commercetools, Salesforce B2B)
3. **Hybrid:** Buy core B2B engine, integrate with custom services

---

## Evaluation Matrix

| Criterion | Weight | Build | Buy | Hybrid |
|------------|--------|--------|------|---------|
| Time to Market | 20% | 3/5 | 4/5 | 4/5 |
| 3-Year Total Cost | 25% | 4/5 | 2/5 | 3/5 |
| Customization Flexibility | 20% | 5/5 | 3/5 | 4/5 |
| Integration Complexity | 15% | 4/5 | 2/5 | 3/5 |
| Strategic Control | 10% | 5/5 | 2/5 | 4/5 |
| Maintenance Burden | 10% | 3/5 | 4/5 | 3/5 |
| **Weighted Score** |  | **4.05** | **2.95** | **3.65** |

---

## Recommendation

**Build within modular commerce core**

---

## Rationale

- B2B pricing and account structures are strategic differentiators
- Better integration with existing commerce logic
- Lower long-term cost than SaaS licensing
- Avoid platform dependency
- Enables incremental rollout

Given internal commerce expertise, this is a high-leverage investment.

---

## Implementation Plan

1. Extract Account domain
2. Build Organization Service
3. Implement Pricing Service (tiered + bulk logic)
4. Add Invoice & Net Terms module
5. Launch pilot with select wholesalers

**Timeline:** Q1–Q2 2026  
**Investment:** ~$500K development effort

---

# Summary Matrix

| Component | Decision | Investment | Timeline |
|------------|-----------|------------|------------|
| Payments | Buy (Global PSP) | ~$50–80K/year | Q2 2025 |
| Multi-Region Database | Hybrid | ~$300K | Q3–Q4 2025 |
| B2B Engine | Build | ~$500K | Q1–Q2 2026 |

---

# Executive Summary of Decisions

| Strategic Area | Approach | Why |
|----------------|----------|------|
| Payments | Buy | Speed + compliance |
| Data Architecture | Hybrid | Compliance + scalability balance |
| B2B Platform | Build | Strategic differentiation |

This approach:

- Minimizes regulatory and operational risk
- Preserves capital for revenue-generating capabilities
- Aligns with evolutionary modernization strategy
- Fits within $2M annual technology budget
- Enables international expansion within 18 months
