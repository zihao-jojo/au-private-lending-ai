# 6. AI Opportunity Areas

## Gap Analysis: Australia vs. Global

| Capability | Global Status | Australia Status | Gap Level |
|---|---|---|---|
| AI document extraction (lending) | Ocrolus (1,600+ doc types) | **Nothing for AU documents** | Critical |
| AI underwriting | Zest AI (300 lenders, 60-80% automation) | **No AU-native solution** | Critical |
| Document fraud detection | Inscribe (AI-generated fraud up 5x) | **No local player** | Critical |
| Agentic AI in lending | Blend Intelligent Origination | Aggregators have basic workflow only | Significant |
| Open banking for lending | Mature in US/UK | CDR live but early; expanding 2026 | Closing |
| Lending marketplace | LendingTree (500+ lenders) | Finder (comparison only), Joust (limited) | Moderate |
| Credit risk ML with alt data | 1,000+ data points common | CCR only 92 providers; alt data nascent | Significant |
| eClosing | Snapdocs (1-in-4 US transactions) | PEXA for settlement only; no eClosing | Significant |

---

## Opportunity 1: AU-Native Document Intelligence Platform

### The Problem
Australian lending requires processing documents that no global platform supports:
- ATO tax returns (ITR), Notice of Assessment (NOA)
- PAYG Payment Summaries / Income Statements
- Business Activity Statements (BAS)
- AU-format bank statements
- Company financials, trust deeds, ASIC extracts
- Superannuation statements
- AU-format payslips (STP Phase 2)

A loan officer processing 5-10 deals/day manually reads **50-300 documents**. No one is automating this for AU documents.

### Technical Approach
1. OCR + LLM pipeline: Google Document AI / AWS Textract → fine-tuned extraction models
2. AU-specific validation rules (TFN format, ABN lookup, ATO form structures)
3. Cross-document verification (income on tax return vs. bank deposits)
4. Fraud detection layer (altered documents, inconsistencies)

### Market Size
Every lender, broker, and aggregator in Australia. Estimated 15,000+ brokers + hundreds of lenders.

### Competition
Minimal. Some global tools (Affinda for payslips, DocuClipper for bank statements) but no comprehensive AU lending document platform.

---

## Opportunity 2: AI Underwriting Engine for Non-Bank Lending

### The Problem
Non-bank lenders use manual or basic scorecard approaches. A loan officer's "underwriting" is often:
1. Open Excel
2. Manually enter borrower data
3. Check Zillow/CoreLogic for property value
4. Calculate LTV/DSCR by hand
5. Make gut-feel decision
6. Write term sheet in Word

This takes 2-5 days per deal. Speed = competitive advantage (especially for caveat/bridging lenders).

### What to Build
Phase 1 — **Rules engine + auto-calculator** (no ML needed):
- Input: property address → auto-pull CoreLogic/PropTrack valuation + comps
- Auto-calculate: LTV, DSCR, risk score based on configurable rules
- Output: approve/decline/review recommendation + suggested rate + auto-generated term sheet

Phase 2 — **AI layer**:
- LLM reads borrower documents, extracts data, fills system
- AI analyzes comp photos, property condition
- Natural language explanation of decisions

Phase 3 — **ML risk model** (after accumulating deal data):
- Predict default probability from CDR data + CCR + property data
- Must be explainable (ASIC requirement): SHAP values, counterfactual explanations

### Target Customers
- Caveat lenders (speed is their selling point)
- Bridging finance providers
- Private credit funds
- Alt-doc specialists (self-employed, ABN holders)

### Data Sources
| Data | Source | Cost |
|------|--------|------|
| Property value + comps | CoreLogic API, PropTrack API | $$ |
| Credit report | Equifax, Experian | $ per pull |
| Company/director info | ASIC registry | Free-$ |
| Bank transactions | CDR (Frollo/Basiq) | $ per consent |
| ATO income verification | Via broker/borrower | Free |

---

## Opportunity 3: CDR-Powered Lending Infrastructure

### The Timing
CDR expands to non-bank lenders from **July 2026**. Most non-banks are NOT prepared. This is a compliance-driven sales opportunity.

### What to Build
Middleware/API layer that:
- Connects non-bank lenders to CDR data via Frollo/Basiq
- Automates income verification from real-time transaction data
- Calculates debt-to-income across all institutions in real-time
- Provides ongoing portfolio monitoring (early warning for defaults)
- Enables action initiation for loan setup (direct debits, account switching)

### Why Now
- Non-banks have 12-18 months to comply
- Building now = first mover advantage
- Frollo and Basiq provide raw data pipes but **don't offer lending-specific decisioning**

---

## Opportunity 4: Intelligent Broker-to-Lender Matching

### The Problem
Brokers handle 76.8% of loans but manually match borrowers to lenders. For non-standard borrowers (self-employed, SMSF, foreign income, trust structures), this means:
- Calling multiple lenders to ask "do you do this?"
- Reading 50+ page policy documents
- Guessing which lender will approve

### What to Build
AI platform that:
- Ingests borrower profile (income docs, credit report, property details)
- Maps against real-time lending policies from 50+ non-bank lenders
- Recommends optimal matches ranked by **probability of approval**
- Auto-generates submission notes and compliance documentation

### Competitive Moat
Requires aggregation of non-bank lender policies (constantly changing, often not machine-readable). First mover who builds this database wins.

### GTM
Partner with 1-2 aggregators. Brokers are already there; you just add intelligence to the existing workflow.

---

## Opportunity 5: Private Lending Origination Platform

### The Problem
Private credit (A$224B market) is largely managed via spreadsheets and email.

### What to Build
Purpose-built digital platform for private/non-bank lenders:
- Digital application portal
- CoreLogic/PropTrack API integration for auto-valuation
- CDR-powered income verification
- Automated credit assessment (rules + ML)
- Digital document execution
- Investor/funder portal for warehouse facilities
- Portfolio dashboard and reporting

### Target
- A$224B private credit market
- Hundreds of non-bank lenders with minimal tech

---

## Opportunity 6: Automated Valuation for Non-Standard Properties

### The Problem
CoreLogic AVM works well for standard residential, but only ~40% of homes can be evaluated solely by AVM. Gaps exist for:
- Development sites
- Rural/regional properties
- Commercial properties
- Strata units with complex factors (defects, levies)

### Technical Approach
- Satellite imagery + planning/zoning data
- Construction cost modeling
- Rental yield modeling
- AU-specific: strata vs. torrens, heritage overlays, bushfire/flood zones, council rates

---

## Opportunity 7: Post-Settlement Portfolio Intelligence

### The Problem
Most non-bank lenders have minimal monitoring of borrower health after settlement.

### What to Build
- CDR data monitoring for early warning (declining income, increasing debt)
- Real-time property value tracking via AVM feeds
- Dynamic LVR calculation across portfolio
- Proactive refinancing triggers
- Hardship indicator detection before default

---

## Priority Ranking

| Opportunity | Market Size | Competition | Technical Difficulty | Time to Revenue |
|---|---|---|---|---|
| 1. Document Intelligence | Large | Very Low | Medium | 6-12 months |
| 2. AI Underwriting | Large | Very Low | Medium-High | 6-12 months |
| 3. CDR Infrastructure | Medium | Low | Medium | 12-18 months |
| 4. Broker-Lender Matching | Large | Low | Medium | 6-12 months |
| 5. Origination Platform | Very Large | Low-Medium | High | 12-24 months |
| 6. Non-Standard AVM | Medium | Medium | High | 18-24 months |
| 7. Portfolio Intelligence | Medium | Very Low | Medium | 12-18 months |

### Recommended Starting Point

**Start with #2 (AI Underwriting) targeting caveat/bridging lenders**, because:
1. Closest to revenue — directly helps lenders make more money faster
2. Small customer base (dozens, not thousands) — manageable sales effort
3. Simple initial product (rules engine, not ML) — fast to build
4. Your wife's real estate network gives you direct access to these lenders
5. Can naturally expand to #1 (Document Intelligence) and #5 (Full Platform)

---

Sources:
- [Ocrolus](https://www.ocrolus.com/)
- [Zest AI](https://www.zest.ai/)
- [Blend Intelligent Origination](https://blend.com/company/newsroom/blend-unveils-vision-intelligent-origination-new-operating-model-lending/)
- [Inscribe AI](https://www.inscribe.ai/)
- [MFAA Broker Market Share](https://www.mfaa.com.au/news/mortgage-broker-market-share-reaches-new-peak)
- [Australia Alternative Lending $33.58B by 2029](https://www.globenewswire.com/news-release/2026/02/19/3240877/28124/en/)
