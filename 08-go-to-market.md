# 8. Go-to-Market Strategies

## Your Unfair Advantage

Your wife works in real estate investment and has direct relationships with private lenders. This is the single most important asset for any of these opportunities — **industry access beats technology every time** in B2B fintech.

## Strategy A: AI Underwriting for Caveat/Bridging Lenders (Recommended Start)

### Why This First
- Caveat lenders compete on **speed** — your tool directly increases their competitive advantage
- Small, concentrated market (dozens of active lenders) — you can talk to all of them
- Simple initial product (rules + API calls, no ML needed)
- Each lender does hundreds of deals/year — clear ROI

### Phase 1: MVP (Month 1-3)

Build a web app:
```
Broker/borrower submits deal
    ↓
Auto-pull CoreLogic/PropTrack valuation
    ↓
Auto-calculate LVR, risk factors
    ↓
Apply lender's rules (configurable per client)
    ↓
Output: approve/decline + suggested rate + term sheet PDF
```

**Tech stack**: Next.js + Supabase + CoreLogic API + PropTrack API. Keep it simple.

### Phase 2: Pilot (Month 3-6)

- Approach **2-3 caveat lenders** through your wife's network
- Free pilot: "Let us process your next 20 deals through the system"
- Goal: prove you can cut their assessment time from days to hours
- Iterate based on their feedback

### Phase 3: Monetize (Month 6-12)

Pricing models:
| Model | Price | When |
|-------|-------|------|
| Per-deal fee | A$50-200/deal | Low volume lenders |
| Monthly SaaS | A$1,000-5,000/month | Medium lenders |
| Enterprise | A$50K+/year | Large non-bank lenders |

### Phase 4: Expand (Year 1-2)

- Add document AI (auto-extract borrower docs)
- Add CDR integration (real-time income verification)
- Expand to bridging, construction, SMSF lenders
- Eventually build full origination platform

---

## Strategy B: Broker-Lender Matching Platform

### GTM via Aggregators

Don't go direct to 15,000 brokers. Partner with aggregators:

1. **Approach one aggregator** (Connective or Finsure — more innovative, non-bank friendly)
2. Offer as a **free add-on** to their existing platform
3. Broker enters deal → your AI matches to best non-bank lenders on the panel
4. Aggregator benefits: more deals flowing to panel lenders = more commission

### Building the Policy Database

The moat is **machine-readable lender policies**. How to build:

1. Start by **manually encoding** policies for 20-30 non-bank lenders
2. Use LLM to parse policy PDFs as they update
3. Build relationships with lender BDMs who notify you of policy changes
4. Over time, offer lenders a portal to **self-update** their policies

### Revenue
- Free for brokers (you are the aggregator's tool)
- Charge lenders for **priority placement** or **qualified lead delivery**
- Eventually: per-funded-deal referral fee (0.1-0.25 points)

---

## Strategy C: Document Intelligence Platform

### GTM: Bottom-Up Adoption

1. Build a **free tier** — brokers upload 5 docs/month free
2. Automatically extract key fields from AU tax returns, bank statements, payslips
3. Output: structured data in CSV/Excel + pre-filled application forms
4. Viral loop: brokers share with other brokers ("this thing saved me 2 hours")

### Scaling
- Free tier → paid plans (A$99-499/month per broker)
- Enterprise deals with aggregators and lenders
- API access for LOS integration

### Technical Approach
```
Document uploaded (PDF/image)
    ↓
Classification (what type of document?)
    ↓
LLM extraction (Claude/GPT with AU-specific prompts)
    ↓
Validation (ABN lookup, TFN format, cross-reference)
    ↓
Structured output (JSON/CSV) + confidence scores
    ↓
Human review for low-confidence fields
```

---

## Key Sales Channels (All Strategies)

### 1. Direct Relationships (Your Wife's Network)
- Private lenders she works with
- Real estate investor networks
- Property developer contacts

### 2. Industry Events
| Event | Why |
|-------|-----|
| AFIA Annual Conference | Senior finance industry decision makers |
| MFAA National Conference | 15,000+ broker members |
| CAFBA events | Commercial finance brokers (your target) |
| Private Credit Forum 2026 | Institutional investors + fund managers |
| Real estate investor meetups | Borrowers who use private lending |

### 3. Online Channels
| Channel | Approach |
|---------|----------|
| LinkedIn | Connect with fund managers, loan officers, broker BDMs |
| Property Chat / Somersoft forums | AU property investor communities |
| Mortgage Professional Australia (MPA) | Industry publication — guest articles |
| The Adviser | Leading broker publication |

### 4. Aggregator Partnerships
- Get your tool on **one aggregator's platform** = access to thousands of brokers
- Start with Connective or Finsure (more innovative, more open to new tools)

---

## Financial Model (AI Underwriting SaaS)

### Conservative Scenario

| Metric | Year 1 | Year 2 | Year 3 |
|--------|--------|--------|--------|
| Paying customers | 5 | 20 | 50 |
| Avg revenue per customer | A$24K | A$36K | A$48K |
| Annual revenue | A$120K | A$720K | A$2.4M |
| Gross margin | 80% | 85% | 85% |

### Cost Structure
| Item | Monthly |
|------|---------|
| Cloud (AWS/GCP) | A$500-2,000 |
| CoreLogic/PropTrack API | A$2,000-5,000 |
| CDR data (Frollo/Basiq) | A$500-2,000 |
| Your time | Sweat equity |

### Key Metric to Track
**Time-to-decision improvement**: If you can prove "assessment went from 3 days to 3 hours", the product sells itself.

---

## Regulatory Considerations for Each Strategy

| Strategy | Licence Needed? | Notes |
|----------|----------------|-------|
| AI Underwriting SaaS (B2B) | **No** — pure technology provider | Lender holds the ACL |
| Broker-Lender Matching | **Maybe** — depends on structure | If recommending specific products, may need ACL as credit assistant |
| Document Intelligence (B2B) | **No** — pure technology provider | Handle borrower data per Privacy Act |

For all strategies:
- **Privacy Act compliance** is non-negotiable (borrower data)
- **SOC 2 Type 2** will be expected by larger clients
- Contact **ASIC Innovation Hub** before launch to confirm licensing position

---

## Timeline

```
Month 1-2:   Validate with 5-10 lenders (conversations, not code)
             → Confirm: what's the #1 pain point?
             → Confirm: would they pay for a solution?

Month 2-4:   Build MVP of chosen strategy
             → CoreLogic/PropTrack API access
             → Basic web app

Month 4-6:   Pilot with 2-3 lenders (free)
             → Measure time-to-decision improvement
             → Iterate based on feedback

Month 6-9:   Start charging pilot customers
             → Refine pricing
             → Case studies from pilots

Month 9-12:  Scale to 5-10 customers
             → Hire first employee (sales or engineering)
             → Start SOC 2 process

Year 2:      20+ customers, A$500K+ ARR
             → Expand product (add doc AI, CDR)
             → Consider seed funding if needed
```

---

## The One Thing to Do First

Before writing any code:

**Talk to 5 private lenders your wife knows. Ask them:**
1. What's the most time-consuming part of processing a loan?
2. How do you currently assess a deal?
3. What would you pay for a tool that cuts assessment time in half?
4. What data do you wish you had but don't?

Their answers will tell you exactly which opportunity to pursue.
