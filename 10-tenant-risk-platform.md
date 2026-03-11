# 10. Pivot: CDR-Powered Tenant Risk Scoring Platform

## Why Not Private Lending AI

After critical analysis, private lending AI is the wrong direction for this team:

| Problem | Detail |
|---------|--------|
| **Market too small** | A few hundred active private lenders in Australia. Even 10% market share = ~20 customers |
| **ML adds little value** | Low frequency (hundreds of deals/year), non-standardized (every deal is different), experienced loan officers outperform models with sparse data |
| **CDR data less relevant** | Asset-backed lending cares about property value and exit strategy, not borrower income patterns |
| **Capital required** | Running a fund needs real money; one bad deal = real losses |
| **Execution mismatch** | Three people with full-time jobs can't run a lending operation on the side |

The core mistake was starting from "private lending" and trying to bolt on AI. The right approach is starting from the team's actual capabilities and finding the market that fits.

---

## The Real Opportunity: Tenant Risk Scoring

### Market Context

- **~3 million rental properties** in Australia
- **~1-1.5 million tenancy applications per year**
- Vacancy rates at historic lows: **1-2%** in major cities
- Bad tenant cost: **A$5,000-30,000+** per incident (unpaid rent, damage, tribunal, vacancy)
- Rental crisis means landlords can't afford mistakes and tenants need to stand out

### How Tenant Screening Works Today (Broken)

```
Tenant applies on realestate.com.au
    → Submits: payslip, bank statement, employment letter, references
    → Agent receives 20-50 applications per listing
    → Runs TICA/NTD check (blacklist database — only past offenders)
    → Maybe runs Equifax TenantCheck (basic credit score)
    → Manually reviews payslips and bank statements
    → Picks someone based on gut feel + limited info
```

**Everything wrong with this:**

1. **Documents are trivially fakeable.** Fake payslips cost $50 online. Bank statements edited with PDF tools. Employment letters from friends. Agents cannot detect this at scale
2. **TICA/NTD is backward-looking.** Only tells you if someone was reported before. Most bad tenants have no prior record. Zero predictive power
3. **Equifax score doesn't reflect rental behavior.** Credit score 750 but chronically late on rent? Equifax doesn't know. Credit score designed for lending, not renting
4. **Manual review of 20-50 applications is unsustainable.** Agents spend hours per listing reviewing documents they can't truly verify
5. **No fraud detection.** Agent has no way to verify if the payslip showing $8,000/month actually matches reality

### What CDR Data Changes

When a tenant consents to share Open Banking data (one-click authorization via Frollo/Basiq), we get **direct-from-bank truth**:

```
INCOME VERIFICATION (unfakeable):
  ✅ Actual salary deposits (amount, frequency, employer name)
  ✅ Income stability over 6-12 months (variance, trend)
  ✅ Multiple income sources identified
  ✅ Self-employment income patterns
  vs. a payslip PDF that anyone can fabricate

RENT PAYMENT HISTORY (the most predictive signal):
  ✅ Current rent amount and payment dates
  ✅ Late payment frequency (how often, how late)
  ✅ Rent-to-income ratio (actual, not stated)
  vs. a reference from a "previous landlord" who might be a friend

FINANCIAL HEALTH:
  ✅ Account balance trend (savings growing or depleting?)
  ✅ Emergency buffer (months of expenses in savings)
  ✅ Existing debt obligations (loan repayments, credit cards)
  ✅ BNPL usage frequency (Afterpay, Zip — overleverage signal)

RED FLAGS:
  🚨 Gambling transactions
  🚨 Payday loan usage (Wagetap, Beforepay — financial stress signal)
  🚨 Frequent dishonours / bounced payments
  🚨 Cash withdrawals >30% of income
  🚨 Sudden income drop in recent months

FRAUD DETECTION:
  🔍 Submitted payslip says $8,000/month — CDR shows $5,000 deposits → MISMATCH
  🔍 Submitted bank statement shows $20K savings — CDR shows $3K → FRAUD
  🔍 Claims to work at Company X — no salary deposits from Company X ABN → FAKE
```

**CDR data cannot be faked. It comes directly from the bank via API.** This single fact eliminates the entire fake document problem.

---

## Why This Perfectly Matches Our Team

| Person | Role | Why It Fits |
|--------|------|------------|
| **Zihao (Block credit/fraud ML)** | Build fraud detection (fake docs vs CDR cross-validation) + risk scoring model | Same problem as Cash App fraud: detect fakes, score risk, real-time decisioning. Directly transferable skills |
| **Friend (Wagetap CDR data science)** | CDR data pipeline, feature engineering from bank transactions, income verification model | This is literally what he does every day at Wagetap — extract income, assess creditworthiness from CDR bank data. Just applying it to rent instead of wage advance |
| **Wife (property investor)** | First user, product validation, sales to PM agents she knows, domain expertise on what makes a good/bad tenant | She IS the customer. She's dealt with tenants, agents, applications. She knows the pain firsthand and has relationships with agents |

### Why ML Actually Works Here (Unlike Private Lending)

| Dimension | Private Lending | Tenant Screening |
|-----------|----------------|-----------------|
| Decision frequency | Hundreds/year per lender | **1-1.5 million/year nationally** |
| Data volume | Too sparse for ML | **Massive** — every application = training data |
| Standardization | Every deal is bespoke | **Highly standardized** — income, rent history, spending patterns |
| Human cost to replace | Experienced loan officer is fast | **Agent reviewing 50 applications is slow and error-prone** |
| ML marginal value | Experienced human may be better | **ML far exceeds human** — can't manually cross-check CDR vs documents at scale, can't process 50 apps in minutes |

---

## Product Design

### Core Product: Tenant Risk Report

```
Agent has a new listing with 30 applicants
    ↓
Sends screening link to all applicants (or embedded in existing application flow)
    ↓
Tenant clicks link → authorizes CDR data sharing (one-click, Frollo/Basiq handles consent)
    ↓
System pulls bank transaction data (typically 3-12 months)
    ↓
Processing pipeline:
    │
    ├── Income Verification Engine
    │   ├── Identify salary deposits (amount, frequency, source)
    │   ├── Calculate income stability score
    │   ├── Cross-reference vs submitted payslip → flag mismatches
    │   └── Output: Verified monthly income ± confidence interval
    │
    ├── Rent History Analyzer
    │   ├── Identify rent payments in transaction history
    │   ├── Calculate on-time payment rate
    │   ├── Detect patterns (always late by X days, deteriorating trend)
    │   └── Output: Rent reliability score
    │
    ├── Financial Health Assessment
    │   ├── Debt-to-income ratio (real, not stated)
    │   ├── Savings buffer (months of expenses)
    │   ├── Spending trend (stable, increasing, decreasing)
    │   ├── Red flag detection (gambling, payday loans, BNPL overuse)
    │   └── Output: Financial stability score
    │
    ├── Fraud Detection Layer (Zihao's specialty)
    │   ├── CDR income vs submitted payslip comparison
    │   ├── CDR balance vs submitted bank statement comparison
    │   ├── Employer verification (ABN match against deposits)
    │   ├── Document metadata analysis (if documents also uploaded)
    │   └── Output: Fraud risk flag (clear / suspicious / likely fraud)
    │
    └── ML Risk Model
        ├── Combines all features above
        ├── Predicts: probability of rent default in next 12 months
        ├── Predicts: probability of lease break
        ├── Predicts: probability of property damage claim
        └── Output: Overall tenant risk grade (A/B/C/D/E)
    ↓
Agent receives report:
  ┌─────────────────────────────────────────────┐
  │ TENANT RISK REPORT — Jane Smith             │
  │                                             │
  │ Overall Grade: A (Low Risk)                 │
  │                                             │
  │ Income: $6,200/month VERIFIED ✓             │
  │   (matches submitted payslip ✓)             │
  │   Stability: High (6-month variance <5%)    │
  │                                             │
  │ Rent History: Excellent                     │
  │   Current rent: $2,400/month                │
  │   On-time rate: 98% (12 months)             │
  │   Rent-to-income: 39%                       │
  │                                             │
  │ Financial Health: Good                      │
  │   Savings buffer: 2.8 months                │
  │   Debt-to-income: 22%                       │
  │   Red flags: None                           │
  │                                             │
  │ Fraud Check: Clear ✓                        │
  │   All submitted documents consistent        │
  │   with bank data                            │
  │                                             │
  │ Recommendation: APPROVE                     │
  └─────────────────────────────────────────────┘

Agent sees all 30 applicants ranked by risk grade → makes decision in 5 minutes instead of 5 hours
```

### Why Tenants Would Consent to CDR Sharing

In a market with 1-2% vacancy and 30+ applicants per listing:
- Sharing CDR data = **verified income, verified rent history, higher trust score**
- This makes your application **stand out** from 29 others who submitted potentially fake documents
- It's a competitive advantage for good tenants
- Similar to how credit scores work: voluntary but practically required

---

## Competitive Landscape

| Player | What They Do | CDR Data? | ML Scoring? | Fraud Detection? |
|--------|-------------|-----------|-------------|-----------------|
| **TICA** | Blacklist database (past offenders only) | No | No | No |
| **NTD** | Blacklist database | No | No | No |
| **Equifax TenantCheck** | Basic credit report | No | No | No |
| **Snug** | Digital rental application platform | No | No | No |
| **2Apply / 1Form** | Application form collection | No | No | No |
| **Ignite (REA Group)** | Rental application via realestate.com.au | No | No | No |
| **Us** | CDR-verified risk scoring + fraud detection | **Yes** | **Yes** | **Yes** |

**Nobody is using CDR data for tenant screening. Zero players. Wide open.**

### Why Incumbents Won't Easily Copy This

1. **TICA/NTD**: Database companies, not tech companies. No ML capability. No CDR integration
2. **Equifax**: Could add CDR, but they're slow, enterprise-focused, and their credit score product is "good enough" for most use cases. Innovation not in their DNA
3. **Snug/2Apply**: Application platforms, not analytics companies. Could partner with us rather than build
4. **REA Group**: Owns PropTrack and 1Form. Could theoretically build this. Biggest threat. But large companies are slow and this is niche for them

### Moat That Grows Over Time

```
More agents use the platform
    → more tenant applications flow through
    → more data to train ML models
    → better risk predictions
    → better outcomes for agents
    → more agents adopt
    → network effect: if multiple agents use it, we see the same tenant
       across applications (richer profile, better fraud detection)
```

---

## Business Model

### Phase 1: Per-Screening Revenue

| Pricing | Who Pays | Notes |
|---------|----------|-------|
| A$15-25 per screening | Agent or landlord | Current market rate for Equifax TenantCheck is ~$15-25. We can price at parity with 10x more value |
| A$5-10 per application | Tenant (optional) | Tenant pays to get a "verified profile" they can reuse across applications |

At 1% market penetration (10,000-15,000 screenings/year): **A$150K-375K ARR**
At 5% (50,000-75,000): **A$750K-1.9M ARR**
At 10% (100,000-150,000): **A$1.5M-3.75M ARR**

### Phase 2: Rent Guarantee Product (The Big Money)

Partner with an insurer or self-underwrite:
- Guarantee landlord receives rent even if tenant defaults
- Price based on our risk score: Grade A tenant = 1.5% of annual rent, Grade C = 4%
- Average annual rent ~A$30,000

At 1% of rental market (30,000 properties):
30,000 × A$30,000 × 2.5% avg premium = **A$22.5M in premium revenue**

This is where the real scale is. The screening product is the wedge; rent guarantee is the business.

### Phase 3: Ongoing Monitoring (SaaS)

- Continuous CDR monitoring of existing tenants
- Alert landlord/agent if tenant's financial situation deteriorates
- "Tenant at 42 Smith St — income dropped 30% last month, savings depleted. Recommend proactive outreach."
- Subscription: A$10-20/property/month
- 10,000 properties monitored: A$1.2-2.4M ARR

### Revenue Trajectory

| Year | Revenue Source | ARR (Conservative) |
|------|--------------|-------------------|
| 1 | Screening fees | A$100-300K |
| 2 | Screening + monitoring | A$500K-1M |
| 3 | Screening + monitoring + rent guarantee | A$2-5M |
| 4+ | Full platform + insurance | A$5-20M |

---

## Technical Architecture

### Stack

| Component | Technology | Owner |
|-----------|-----------|-------|
| CDR data pipeline | Basiq or Frollo API (accredited intermediary) | Friend (Wagetap CDR expertise) |
| Transaction categorization | Rule-based + ML classifier for AU bank transactions | Friend |
| Income verification engine | Pattern matching on salary deposits + statistical models | Friend |
| Fraud detection | Document analysis + CDR cross-reference + anomaly detection | Zihao (Block fraud expertise) |
| Risk scoring model | XGBoost/LightGBM → logistic regression for explainability | Zihao + Friend |
| API layer | FastAPI (Python) or Node.js | Zihao |
| Frontend (agent dashboard) | Next.js / React | Zihao |
| Database | PostgreSQL + Redis cache | Standard |
| Hosting | AWS or GCP | Standard |
| Model monitoring | MLflow or similar | Zihao (Block MLOps expertise) |

### CDR Integration (Friend's Domain)

```
Tenant consent flow:
  1. Agent sends screening link to tenant
  2. Tenant clicks → redirected to CDR consent page (Basiq/Frollo hosted)
  3. Tenant selects their bank → logs in → authorizes data sharing
  4. CDR API returns 3-12 months of transaction data
  5. Our system processes and scores

Data fields from CDR:
  - Transaction date, amount, description, category
  - Account balance (current and historical)
  - Account type (savings, transaction, credit card)
  - Account holder name and details

No need to become an ADR ourselves — use Basiq or Frollo as intermediary.
Frollo handles 95%+ of AU open banking activity.
```

### ML Model Cold Start (How to Train Without Historical Tenant Data)

**Stage 1: Rules engine (Day 1)**
No ML needed. Encode domain knowledge:
```python
# Example rules
risk_score = 0

# Income verification
if cdr_income matches submitted_payslip within 10%:
    risk_score += 0  # consistent
else:
    risk_score += 30  # mismatch = major red flag

# Rent payment history
on_time_rate = calculate_rent_on_time_rate(transactions)
if on_time_rate > 0.95:
    risk_score -= 10  # excellent history
elif on_time_rate < 0.80:
    risk_score += 20  # poor history

# Financial stress signals
if has_payday_loans(transactions):
    risk_score += 15
if has_gambling(transactions):
    risk_score += 20
if savings_buffer_months < 1:
    risk_score += 10

# Rent affordability
rent_to_income = monthly_rent / verified_monthly_income
if rent_to_income > 0.35:
    risk_score += 10
if rent_to_income > 0.45:
    risk_score += 20
```

**Stage 2: Supervised learning (after 500-1,000 screenings)**
- Track outcomes: did the tenant get approved? Did they default? Did they break lease?
- Outcome data available 6-12 months after screening
- Initial model: logistic regression (interpretable, works with small data)
- Features: CDR income stability, rent payment history, savings buffer, debt ratio, fraud signals

**Stage 3: Richer models (after 5,000+ screenings)**
- Gradient boosted trees (XGBoost/LightGBM)
- More features: transaction-level patterns, seasonal effects, macro indicators
- A/B test model vs rules engine

---

## Regulatory and Compliance

### Licensing

**No credit licence (ACL) needed.** We are providing an information/assessment service, not providing credit or acting as a credit intermediary.

**No AFSL needed** unless we launch the rent guarantee product as a financial product (Phase 2+).

### Privacy Act

- Must comply with Australian Privacy Principles (APPs)
- Credit-related information has additional protections under Part IIIA of the Privacy Act
- **Key requirement**: Clear consent from tenant for CDR data access (handled by Frollo/Basiq consent flow)
- Must have a privacy policy explaining data use
- Must allow tenants to access and correct their data
- Notifiable Data Breaches scheme applies

### State Tenancy Laws

Each state has specific rules about tenant screening:
- **NSW**: Landlords can request information "reasonably necessary" to assess application
- **VIC**: More restrictive — can only ask for information "reasonably necessary" and cannot discriminate on prohibited grounds
- **QLD**: Similar to NSW
- **General**: Cannot discriminate based on race, gender, disability, family status, etc.

**CDR-based scoring must be carefully designed to avoid proxy discrimination.** ML model must be audited for bias (Zihao's experience with fairness in credit models at Block is directly applicable).

### Anti-Discrimination Compliance

- Risk model must not use protected attributes (even indirectly)
- Regular bias audits
- Explainable decisions (tenant has right to know why they were scored a certain way)
- This is an area where Zihao's Block experience is valuable — financial services bias auditing is a well-established practice

---

## Go-to-Market

### Phase 1: Wife's Network (Month 1-4)

```
Wife's own property manager
    → "Hey, I built a tool that verifies tenant income from their bank data.
        No more fake payslips. Want to try it on your next listing?"
    → Free pilot, 1-2 listings
    → Get feedback, iterate

Other investors she knows
    → Their property managers
    → Same pitch
    → Target: 3-5 PM agencies in pilot
```

### Phase 2: Local Expansion (Month 4-8)

```
Case studies from pilot:
    "PM Agency X used our tool. Found 3 fake payslips out of 40 applications.
     Selected tenants had zero late payments in first 6 months."

Use case studies to approach:
    → Other PM agencies in same city
    → Real estate investor meetups / Facebook groups
    → Property management industry events
```

### Phase 3: Platform Integration (Month 8-12)

```
Build API/plugin for existing PM software:
    → PropertyMe (dominant AU PM software)
    → Console Cloud
    → MRI Property Central
    → Rex

Or partner with application platforms:
    → Snug
    → 2Apply

Agent doesn't need to change their workflow — our scoring appears
inside tools they already use.
```

### Phase 4: Scale (Year 2+)

```
Sales channels:
    → PM industry conferences (REIQ, REINSW, REIV)
    → PM franchise networks (Ray White, LJ Hooker, Harcourts, Barry Plant)
    → Direct sales to large PM companies (hundreds of managed properties each)
    → Content marketing (blog, case studies, industry publications)
```

### Key Industry Contacts

| Organization | Relevance |
|-------------|-----------|
| **REINSW** (Real Estate Institute NSW) | Industry body, events, credibility |
| **REIV** (Real Estate Institute Victoria) | Same for VIC |
| **REIQ** (Real Estate Institute Queensland) | Same for QLD |
| **PropertyMe** | Dominant PM software — integration partner |
| **Domain / REA Group** | Listing platforms — potential integration or acquisition |
| **Real Estate Business (REB)** | Industry media — PR channel |

---

## Expansion Path

```
Year 1: Tenant screening (CDR verification + risk scoring)
            ↓
Year 2: + Ongoing tenant monitoring (CDR alerts)
        + Rent guarantee insurance (partner with insurer)
            ↓
Year 3: + Portable tenant profile (tenant carries verified history between applications)
        + Landlord insurance integration
        + Expand to NZ (similar market, CDR equivalent coming)
            ↓
Year 4+: + Commercial tenant screening (bigger deal sizes)
         + Expand to UK (Open Banking mature, similar rental crisis)
         + Data products (rental market intelligence)
```

### The Endgame Vision

A world where:
- Tenants build a **verified rental reputation** (like a credit score but for renting)
- Landlords have **real-time visibility** into tenant financial health
- Agents make decisions in **minutes with verified data**, not hours with fake documents
- Rent defaults drop because **risk is properly assessed and priced**

---

## Risks and Mitigations

| Risk | Severity | Mitigation |
|------|----------|-----------|
| **Tenants refuse CDR consent** | Medium | In a 1-2% vacancy market, tenants who share data get preferred. Verified = competitive advantage. Frame as "get approved faster" not "share your data" |
| **Agents resist new tools** | Medium | Don't replace their workflow — embed into existing PM software via API/plugin. Zero behavior change required |
| **REA Group builds this** | High | Move fast, build brand with agents. REA is slow on niche products. Could become acquisition target (positive outcome) |
| **Equifax adds CDR scoring** | Medium | Equifax is slow, enterprise-focused. We'll have agent relationships and better UX by the time they move |
| **Privacy backlash** | Low-Medium | Transparent consent, clear data use explanation, tenant controls. CDR framework already handles consent securely |
| **Bias/discrimination claims** | Medium | Regular model audits, explainable scoring, no protected attributes. Zihao's Block fairness experience |
| **Regulatory changes to tenant screening** | Low | Stay close to state tenancy regulators. Our CDR-based approach is MORE fair than gut-feel (demonstrable) |
| **CDR data quality issues** | Low | Friend's Wagetap experience means he knows which banks have good/bad CDR data. Build fallbacks for gaps |

---

## First Steps

### This Week
1. **Zihao**: Check Block employment contract re: side projects and IP ownership
2. **Friend**: Check Wagetap contract re: same. Also: assess Basiq vs Frollo for CDR integration (he probably already has opinions)
3. **Wife**: Talk to her property manager: "How do you screen tenants? What's the biggest headache? Would you try a tool that verifies income directly from the bank?"

### If All Three Are In
- Create shared repo
- Zihao: Set up basic web app scaffold
- Friend: Build CDR data pipeline prototype (Basiq sandbox has test data)
- Wife: Line up 2-3 PM agents for pilot
- Target: Working prototype in 4-6 weekends
