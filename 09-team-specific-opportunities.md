# 9. Team-Specific Opportunities

## Our Team

| Person | Background | Core Skill |
|--------|-----------|------------|
| **Zihao** | Block (Square/Cash App) — Credit & Fraud ML Modeling | ML pipeline, feature engineering, fraud detection, model monitoring, risk modeling at scale |
| **Friend** | Wagetap — Lead Data Scientist, CDR/Open Banking credit models | Australian CDR data, income verification from bank transactions, credit scoring with alternative data |
| **Wife** | Real estate investor, connected to private lenders and brokers | Deal flow, industry relationships, understands lender pain points firsthand |

This combination is rare in Australia: **ML engineering at fintech scale + CDR data expertise + real estate industry access.**

---

## The Insight

Private lenders in Australia have **no data-driven risk models**. Their current process:

```
Loan officer receives deal
    → Pull Equifax credit score
    → Check property value on CoreLogic
    → Gut feel decision
    → Set interest rate based on "experience"
```

No ML models. No CDR data. No systematic fraud detection. Meanwhile:
- Private lending fraud rates are significantly higher than bank lending
- AI-generated fake documents are growing 5x year-over-year (Inscribe data)
- ASIC is tightening oversight (Report 814) and demanding systematic risk processes
- CDR expands to non-bank lenders July 2026, creating new data possibilities

**We can build risk infrastructure that doesn't exist in Australian private lending.**

---

## Direction A: Credit Decisioning API (B2B SaaS)

### What It Is

An API that private lenders integrate into their workflow to get ML-powered credit decisions.

### How It Works

```
Lender submits deal via API or web portal
    ↓
System pulls data:
  - CDR bank transactions (via Frollo/Basiq) → income patterns, spending, existing debt
  - Equifax/illion credit report → credit history, defaults, enquiries
  - CoreLogic/PropTrack → property valuation, comparable sales
  - ASIC registry → company/director verification
    ↓
ML models run:
  - Probability of Default (PD) model
  - Loss Given Default (LGD) model — incorporating property collateral value
  - Fraud risk score
  - Income stability score (from CDR transaction patterns)
    ↓
API returns:
  - Risk grade (A/B/C/D/E)
  - Suggested interest rate (risk-based pricing)
  - Fraud risk flags
  - Key risk factors with explanations (SHAP-based, ASIC-compliant)
  - Recommended LVR cap
```

### Why Lenders Would Pay

- Private lending bad debt rates ~2-5%. A lender doing A$50M/year at 3% bad debt = A$1.5M losses
- If the model reduces bad debt to 1.5%, that's **A$750K saved per year**
- Charge A$50-100K/year for the API → clear ROI
- ASIC regulatory pressure means lenders need to demonstrate systematic risk assessment
- "We use ML-powered credit decisioning" is a selling point to investors in their fund

### Technical Stack

| Component | Technology | Source |
|-----------|-----------|--------|
| CDR data pipeline | Frollo or Basiq API | Friend's expertise (Wagetap uses this daily) |
| Credit bureau integration | Equifax/illion API | Standard integration |
| Property data | CoreLogic or PropTrack API | Enterprise agreement needed |
| ML models | Python, XGBoost/LightGBM, deployed on AWS/GCP | Zihao's expertise (Block-grade ML ops) |
| Explainability | SHAP values, counterfactual explanations | Required for ASIC compliance |
| Fraud detection | Document analysis + cross-reference models | Zihao's expertise (Block fraud systems) |
| API layer | FastAPI or similar, RESTful | Standard engineering |

### Revenue Model

| Tier | Price | What They Get |
|------|-------|--------------|
| Per-decision | A$50-150/decision | Pay as you go, low commitment |
| Monthly SaaS | A$3-8K/month | Unlimited decisions, dashboard, reporting |
| Enterprise | A$80-150K/year | Custom model tuning, dedicated support, portfolio monitoring |

### Cold Start Problem: No Historical Lending Data

This is the biggest challenge. How to train models without historical loan performance data?

**Solutions:**
1. **Transfer learning from Block/Wagetap**: General credit risk patterns transfer across domains. Income stability, spending patterns, debt ratios are universal risk signals
2. **Start with rules + CDR features**: Use CDR data to build rule-based scoring first (e.g., irregular income = higher risk, high gambling spend = red flag). No ML needed initially
3. **Use public/industry data**: APRA publishes aggregate loss rates by loan type. Academic papers on Australian mortgage default predictors exist
4. **Earn data through the fund (Direction B)**: Every deal we do ourselves generates labeled training data
5. **Offer free/cheap to first 5 lenders**: In exchange for anonymized historical deal data (funded deals + defaults)

---

## Direction B: Tech-Driven Private Lending Fund

### What It Is

Instead of selling tools to lenders, **be the lender**. Use ML as an internal competitive advantage.

### How It Works

```
Wife sources deals through her network
    ↓
Borrower/broker submits application
    ↓
Our ML system:
  - Verifies income via CDR (no manual bank statement review)
  - Scores credit risk (PD model)
  - Detects fraud (document verification + cross-referencing)
  - Assesses property (CoreLogic/PropTrack AVM + market data)
  - Runs financial model (LVR, DSCR, exit strategy assessment)
    ↓
Automated decision: approve/decline/refer to human
    ↓
If approved: auto-generate term sheet with risk-based pricing
    ↓
Fund the loan, earn interest spread
```

### Why This Could Work

| Traditional Private Lender | Us |
|---|---|
| Assesses deal in 2-5 days | Assesses in hours (speed wins deals) |
| Relies on gut feel | Data-driven decisions (lower bad debt) |
| Manual document review | AI-powered extraction + fraud detection |
| Static pricing (everyone gets similar rate) | Risk-based pricing (better risk = lower rate, attract better borrowers) |
| High operating cost (loan officers) | Lower cost (automation) |
| Raises capital based on track record | Raises capital based on track record + transparent risk metrics |

### Fund Economics

| Metric | Conservative | Moderate |
|--------|-------------|----------|
| AUM Year 1 | A$5M | A$10M |
| AUM Year 2 | A$15M | A$30M |
| AUM Year 3 | A$30M | A$60M |
| Weighted avg interest rate | 12% | 12% |
| Cost of capital | 7% | 7% |
| Net interest margin | 5% | 5% |
| Gross profit Year 1 | A$250K | A$500K |
| Gross profit Year 2 | A$750K | A$1.5M |
| Gross profit Year 3 | A$1.5M | A$3M |
| Bad debt provision (1.5%) | -A$75K → -A$450K | -A$150K → -A$900K |

### Starting Capital Options

| Source | Amount | Notes |
|--------|--------|-------|
| Personal savings | A$200-500K | Enough for 1-3 small deals to prove concept |
| Family & friends | A$500K-2M | Common for fund seeding |
| Wholesale investors | A$2-10M | Need track record first (even 6-12 months of self-funded deals) |
| Warehouse facility from larger fund | A$5-20M | La Trobe, Qualitas, Metrics do this for smaller originators |

### Licensing

| Path | When Needed | Cost |
|------|------------|------|
| Commercial purpose only | If all loans are business/commercial purpose | No ACL needed. Use Regulation 68 declarations |
| ACL | If any consumer lending (residential investment by individuals) | A$2-5K application + compliance setup A$20-50K |
| AFSL | If pooling external investor money into a fund | A$5-10K application + compliance setup A$50-100K |

**Starting with commercial-purpose-only lending (caveat, bridging for business) avoids all licensing initially.**

### Phase Plan

```
Phase 1 — Validate (Month 1-6, keep day jobs):
  - Wife identifies 2-3 small deals (A$100-300K each)
  - Fund with personal capital
  - Build basic credit scoring + fraud check pipeline
  - Test: does our assessment match reality?
  - Track: speed to decision, borrower feedback, repayment behavior

Phase 2 — Scale slowly (Month 6-18):
  - If Phase 1 works, do 10-20 more deals
  - Start building ML models with real data
  - Bring in outside capital (friends/family/wholesale)
  - Set up proper fund structure (lawyer: A$15-25K)
  - One person goes full-time (probably wife, she's the deal sourcer)

Phase 3 — Grow (Month 18-36):
  - A$10-30M AUM
  - Full ML pipeline: CDR credit scoring + fraud detection + automated valuation
  - Hire a loan officer / operations person
  - Start licensing the technology to other lenders (Direction A becomes a spin-off)
  - Consider AFSL if raising institutional capital
```

---

## Direction C: Property Lending Fraud Detection

### What It Is

A specialized fraud detection platform for mortgage and property lending, focused on Australian documents and patterns.

### The Problem

Private lending fraud is rampant and getting worse:

| Fraud Type | Description | Detection Method |
|---|---|---|
| **Fake bank statements** | AI-generated or manually altered PDFs | Metadata analysis, font consistency, pixel-level inspection, CDR cross-reference |
| **Inflated income** | Fake payslips, altered tax returns, fabricated BAS | CDR income verification, ATO data cross-reference, employer ABN verification |
| **Valuation fraud** | Colluding with valuers to inflate property value | AVM cross-check, comparable sales analysis, photo analysis |
| **Straw buyers** | Using a front person to borrow | Identity verification, behavioral analysis, relationship mapping |
| **Multi-loading** | Applying to multiple lenders simultaneously | Cross-lender data sharing network (if multiple lenders use the platform) |
| **Fabricated entities** | Fake companies used as borrowers | ASIC registry verification, ABN age check, director cross-reference |
| **AI-generated documents** | Entirely synthetic documents created by AI | Deep learning detection models, document forensics |

### How It Works

```
Lender uploads borrower documents (PDF/images)
    ↓
Layer 1 — Document Forensics:
  - PDF metadata analysis (creation tool, modification dates)
  - Font consistency check
  - Image manipulation detection (ELA — Error Level Analysis)
  - Template matching against known legitimate formats
    ↓
Layer 2 — Data Extraction + Cross-Reference:
  - OCR extract all financial data
  - Compare bank statement income vs CDR real transaction data
  - Verify employer ABN against ASIC registry
  - Check property value against AVM (flag if stated value >> AVM)
    ↓
Layer 3 — Pattern Detection:
  - Behavioral anomaly detection (unusual transaction patterns)
  - Network analysis (connections between applicants, properties, entities)
  - Historical fraud pattern matching
    ↓
Output:
  - Fraud risk score (0-100)
  - Specific flags with evidence
  - Confidence level per flag
  - Recommended actions
```

### Why This Is Uniquely Suited to Us

- **Zihao's Block fraud experience**: Cash App deals with massive scale fraud detection. The same techniques (behavioral analysis, network graphs, anomaly detection) apply directly
- **Friend's CDR expertise**: The killer feature is **CDR cross-referencing** — compare what the borrower submitted (bank statements) against what CDR actually shows. If they don't match, it's fraud. No other Australian tool does this
- **Wife's industry knowledge**: She knows what real deals look like vs. suspicious ones. Domain expertise for feature engineering and validation

### No Competition in Australia

- **Inscribe** (US): Doesn't support Australian document formats
- **Ocrolus** (US): Has some fraud detection but US-only
- **No Australian-native solution exists**
- Banks have internal fraud teams but private lenders don't

### Revenue Model

| Model | Price | Target |
|-------|-------|--------|
| Per-document check | A$5-20/document | Small lenders, pay-as-you-go |
| Per-application | A$50-200/application | Medium lenders |
| Monthly subscription | A$2-5K/month | Larger non-bank lenders |
| Enterprise | A$50-100K/year | Top-tier non-bank lenders, aggregators |

### Network Effect Moat

If multiple lenders use the platform, we can detect **multi-loading** (same borrower applying to multiple lenders). This creates a data network effect — the more lenders on the platform, the better the fraud detection for everyone. This is how credit bureaus became powerful, and it's how a fraud detection network could too.

---

## Combined Strategy (Recommended)

### The Play

Don't pick one direction — **they're all the same thing at different zoom levels.**

```
         Direction C (Fraud Detection)
              ↓ feeds into
         Direction A (Credit Decisioning API)
              ↓ powers
         Direction B (Our Own Fund)
              ↓ generates
         Training data that improves A and C
```

### Concrete Plan

```
Month 1-3: VALIDATE
├── Wife finds 2-3 small deals
├── Zihao builds basic fraud check (document forensics + CDR cross-ref)
├── Friend builds CDR credit scoring prototype
├── Fund deals with personal capital (A$200-500K)
├── All done nights/weekends, keep day jobs
└── Goal: prove the ML adds value vs. gut feel

Month 3-6: BUILD
├── If validation works, formalize the models
├── Build a simple web portal (deal submission + automated assessment)
├── Do 5-10 more deals through the fund
├── Start collecting labeled data (good deals vs. problems)
└── Goal: working prototype of the full pipeline

Month 6-12: MONETIZE
├── Fund: scale to A$2-5M with outside capital
├── API: offer the credit/fraud system to 2-3 other lenders (wife's contacts)
├── Free or cheap initially, in exchange for data + feedback
└── Goal: revenue from both lending spread AND SaaS

Month 12-24: SCALE
├── Fund: A$10-30M AUM, proper fund structure
├── API: 5-10 paying lender clients
├── Fraud network: cross-lender fraud detection
├── One or two people go full-time
└── Goal: A$500K-1M combined revenue (spread + SaaS)

Month 24-36: GROW
├── Fund: institutional capital (super funds interested in private credit)
├── API: expand to mortgage brokers and aggregators
├── Consider: spin off tech as separate company
├── Consider: expand to NZ, SE Asia
└── Goal: A$2-5M combined revenue
```

### Why This Combined Approach Wins

1. **The fund is your first customer**: No cold start problem for the API. You eat your own cooking
2. **Real deal data trains better models**: Every deal you fund generates labeled data. No other API company has this
3. **Credibility sells**: "We use this model ourselves to manage A$XM in loans" is 10x more convincing than "trust our model"
4. **Two revenue streams**: Lending spread (higher but capital-intensive) + SaaS (lower but scalable and capital-light)
5. **Your team covers all bases**: ML (Zihao), CDR data (friend), deal flow + industry (wife)

---

## Key Risks

| Risk | Mitigation |
|------|-----------|
| **Small market** (AU private lending) | Start here, expand to NZ/UK/SE Asia. Or go deep (full-stack platform) |
| **CoreLogic API cost** | Start with PropTrack (may be cheaper). Negotiate volume pricing as you scale |
| **No historical data for ML** | Start with rules, earn data through the fund. 50-100 deals = enough for initial models |
| **Regulatory change** | ASIC tightening actually helps us (lenders need better risk tools). Stay close to ASIC Innovation Hub |
| **One of us leaves day job too early** | Don't. Keep day jobs for 12+ months. Fund small deals on the side. Only go full-time when revenue justifies it |
| **CDR data quality/coverage** | Use CDR + traditional docs as fallback. CDR coverage improving rapidly (mandatory for all banks, non-banks from 2026) |
| **Conflict of interest with employers** | Check employment contracts. Block and Wagetap are not in AU private lending — likely no conflict, but verify |

---

## First Step

**This week:**
1. Zihao: Check Block employment contract re: side projects and IP
2. Friend: Check Wagetap employment contract re: same
3. Wife: Identify one real deal that she can bring to the table
4. All three: Meet for dinner, align on interest level and commitment

**If all three are in:**
- Set up a shared repo
- Wife brings the first deal
- Zihao + friend build the assessment pipeline over 2-3 weekends
- Fund it with personal money
- See what happens

The best way to validate is not more research — it's **doing one deal.**
