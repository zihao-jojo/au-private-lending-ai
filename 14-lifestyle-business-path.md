# 14. The Realistic Path: A$500K-2M/Year Lifestyle Business

## Reframing the Goal

Not building a VC-backed startup. Not trying to IPO. Building a **small, profitable business** that generates A$500K-2M/year in revenue.

This changes everything:
- "Market too small" → **You only need 20-50 customers**
- "Incumbents exist" → **You just need to be better for a niche**
- "Can't raise money" → **Don't need to**
- "Can't compete with Equifax" → **Don't need to. Equifax serves thousands. You serve 30.**

## The Math

| Model | Customers | Price | Revenue |
|-------|-----------|-------|---------|
| 20 lenders × A$3K/month | 20 | A$36K/yr | A$720K |
| 50 brokers × A$400/month | 50 | A$4.8K/yr | A$240K |
| 10 consulting clients × A$150K | 10 | A$150K/yr | A$1.5M |
| 200 brokers × A$200/month | 200 | A$2.4K/yr | A$480K |

Any combination gets you to A$500K-2M. The Australian market has hundreds of lenders and 15,000+ brokers. You only need a tiny slice.

---

## Recommended Path: Consulting → Product

### Phase 1: Consulting (Month 1-6) → A$300-500K/year

#### What You Sell

"I build credit risk models and fraud detection systems for Australian fintechs."

Your Block resume is the only sales asset you need. You've built production ML systems at one of the world's largest fintech companies. In Australia, there are maybe a few dozen people with this specific experience.

#### Who Buys

| Client Type | What They Need | Budget |
|-------------|---------------|--------|
| **Small fintech lenders** (Prospa, Moula, Lumi scale) | Better credit models, fraud detection, model monitoring | A$100-200K/project |
| **Non-bank lenders** going digital | First ML pipeline for credit decisioning | A$50-150K/project |
| **BNPL companies** under new regulation | Affordability assessment models, CCR integration | A$100-200K/project |
| **EWA providers** (Beforepay competitors) | CDR-based income verification models | A$50-100K/project |
| **Insurers** building fraud detection | Claims fraud ML, document verification | A$100-300K/project |
| **Banks** (innovation teams) | Prototype new CDR-powered products | A$150-300K/project |

#### How You Get Clients

**Week 1-2:**
- Update LinkedIn: "Credit Risk & Fraud Detection ML | Ex-Block (Square/Cash App) | Ex-MYOB | Available for consulting"
- Write 2-3 LinkedIn posts about credit ML topics (e.g., "What I learned building fraud models at Block", "CDR data for credit scoring: practical lessons")
- These posts will get attention — the AU fintech community on LinkedIn is small and engaged

**Week 3-4:**
- DM 10-15 CTOs/heads of data at AU fintechs
- Attend 1-2 fintech meetups in Sydney/Melbourne
- Reach out to former MYOB colleagues — they know people in the ecosystem

**Month 2-3:**
- First client (probably A$50-100K project)
- Deliver well, ask for referrals
- In the AU fintech world, 2-3 good projects = everyone knows you

#### Pricing

| Engagement | Rate | Notes |
|-----------|------|-------|
| Advisory / part-time | A$250-400/hour | 10-20 hrs/week alongside day job |
| Project-based | A$50-200K per project | Defined scope and deliverables |
| Fractional Head of ML | A$2-4K/day | 2-3 days/week for one client |

**Note on Block employment:** Check your employment contract. Most tech companies allow consulting outside work hours if it doesn't compete directly. Block/Afterpay does BNPL — consulting for a private lender on credit modeling likely doesn't compete. But verify first.

#### Can You Do This While at Block?

Yes, if:
- No conflict with Block's business (avoid Afterpay competitors)
- Done outside work hours
- No Block IP used
- Employment contract doesn't prohibit it

Many senior engineers do advisory/consulting on the side. 10 hours/week is manageable.

### Phase 2: Spot the Pattern (Month 3-12)

While consulting, you'll notice **every client has the same 2-3 problems**. These become your product ideas.

Possible patterns you might see:
- "Every lender asks me to build the same CDR income verification pipeline" → productize it
- "Everyone needs document fraud checking but can't afford to build it" → SaaS tool
- "Every non-bank lender does credit assessment in Excel" → simple underwriting tool
- "Nobody has good model monitoring for their credit models" → MLOps for fintech

**You won't know which pattern until you're in the room with clients.** This is why consulting first is better than guessing from market research.

### Phase 3: Build the Product (Month 6-18)

Take the most common consulting request and turn it into a self-serve product.

Example: if 4 out of 5 clients asked for CDR income verification:

```
ConsultingVersion:
  - Custom pipeline built for each client
  - A$100K per project
  - Doesn't scale (your time is the bottleneck)

ProductVersion:
  - SaaS: client integrates your API
  - A$2-4K/month subscription
  - Scales without your time
  - 30 clients = A$720K-1.4M/year
```

### Phase 4: Transition (Month 12-24)

```
Month 12:  Revenue = A$400K consulting + A$100K product = A$500K
Month 18:  Revenue = A$200K consulting + A$400K product = A$600K
Month 24:  Revenue = A$100K consulting + A$800K product = A$900K
```

Consulting shrinks as product grows. Eventually product carries the business and consulting becomes optional (or premium priced for strategic clients).

---

## Alternative: Skip Consulting, Go Straight to Product

If consulting doesn't appeal, go straight to building. But keep it small.

### Product A: Private Lender Underwriting Tool

Revisiting this with A$500K-2M framing. Previously killed because "market too small." But 20-30 clients is enough.

```
Target: Caveat lenders, bridging finance, private credit funds
Product: Web app — enter property address + borrower info → auto-assess → term sheet

Features:
  - CoreLogic/PropTrack API for instant property valuation
  - Configurable rules per lender (LVR limits, rate tiers, region restrictions)
  - Auto-generate term sheet PDF
  - Basic borrower document collection portal
  - Dashboard: pipeline, portfolio, reporting

Pricing: A$2-4K/month
Customers needed: 20-30
Revenue: A$480K-1.4M/year

GTM: Wife introduces you to 5 lenders she knows → pilot → word of mouth
Tech: Next.js + Supabase + CoreLogic API. One person can build MVP.
Timeline: 2-3 months to MVP, 6 months to first paying customer
```

### Product B: Document Fraud Checker

```
Target: Mortgage brokers, PM agents, lenders, employers, HR
Product: Upload document → AI checks authenticity → report

Features:
  - PDF metadata analysis (creation tool, edit history, timestamps)
  - Font consistency analysis
  - Image manipulation detection (ELA)
  - Template matching (known ATO form formats, major bank statement formats)
  - LLM-powered content analysis (do the numbers make sense?)
  - Cross-document consistency (does the payslip match the bank statement?)

Pricing:
  - Self-serve: A$200-500/month for unlimited checks
  - Enterprise: A$2-5K/month with API access

Customers needed: 100-200 (self-serve) or 20-50 (enterprise)
Revenue: A$240K-1.2M/year (self-serve) or A$480K-3M/year (enterprise)

GTM:
  - Wife's network for initial PM agent and lender customers
  - LinkedIn content about document fraud (CBA's A$1B scandal is great hook)
  - Broker industry events (MFAA, FBAA conferences)

Tech: Python + Claude/GPT Vision API + PDF analysis libraries + Next.js frontend
Timeline: 2-3 weekends for MVP, 3-6 months to paying customers
```

### Product C: Broker Cash Flow Report Tool

```
Target: Mortgage brokers
Product: Client authorizes CDR → auto-generate lender-ready cash flow report

Features:
  - CDR integration (via Basiq or Frollo)
  - Auto-categorize income, expenses, debts
  - Calculate DTI, savings buffer, income stability
  - Output: standardized PDF that lenders accept
  - Replace manual "collect 3 months of bank statements and squint at them"

Pricing: A$20-30 per report or A$200-400/month subscription
Customers needed: 200-500 brokers
Revenue: A$480K-2.4M/year

GTM: Partner with one aggregator (Connective/Finsure) → instant broker distribution
Tech: Next.js + Basiq API + PDF generation
Timeline: 1-2 months for MVP (friend's CDR expertise makes this fast)

Risk: Basiq already offers something similar. Need to differentiate on UX and broker-specific features.
```

---

## Comparison

| Path | Time to Revenue | Risk | Revenue Potential | Effort |
|------|----------------|------|-------------------|--------|
| **Consulting** | 1-2 months | Very low | A$300K-1.5M | 10-20 hrs/week |
| **Underwriting tool** | 6-12 months | Medium | A$500K-1.5M | Significant |
| **Document fraud checker** | 3-6 months | Medium | A$500K-2M | Moderate |
| **Broker cash flow report** | 3-6 months | Medium-High | A$500K-2M | Moderate |
| **Consulting → Product** | 1 month + 12 months | Low | A$500K-2M | Grows gradually |

---

## My Recommendation

**Start consulting this month.** Keep your Block job. 10 hours/week on the side.

Why:
1. **Immediate cash flow** — no months of building with zero revenue
2. **Learn the market from the inside** — stop guessing, start knowing
3. **Build reputation** — "the credit/fraud ML guy" in AU fintech circles
4. **Spot the real product opportunity** — it'll come from client conversations, not research
5. **Zero risk** — worst case you made A$50-100K extra and learned a lot

The product will emerge. You don't need to pick it today.

---

## First Steps

### This Week
1. Check Block employment contract re: outside consulting
2. Update LinkedIn profile with consulting positioning
3. Write one LinkedIn post about credit ML (the CBA A$1B fraud scandal is perfect hook material)
4. Message 5 former MYOB colleagues: "Hey, I'm doing some consulting on credit/fraud ML. Know anyone who might need help?"

### This Month
1. Land first consulting conversation
2. Meet your friend (Wagetap) — align on whether he wants to be involved
3. Talk to wife's lender contacts: "What's your biggest operational headache right now?"

### Month 2-3
1. First paid consulting engagement
2. Start noticing patterns in what clients need
3. Consider whether a product makes sense

### Month 6
1. Decision point: keep consulting, build a product, or both
2. By now you'll know 10x more about the market than any research document can tell you
