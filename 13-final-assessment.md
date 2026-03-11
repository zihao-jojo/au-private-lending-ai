# 13. Final Assessment: What's Actually Worth Doing

## Everything We Explored

| Direction | Verdict | Why |
|-----------|---------|-----|
| Private lending AI (SaaS for lenders) | Dead | Market too small, ML overkill, lenders don't want it |
| Private lending fund | Dead | Capital risk, licensing, can't do on the side |
| Broker-lender matching platform | Dead | Cold start problem, double-sided market |
| Development site feasibility AI | Dead | Too heavy, Archistar spent 10+ years, CoreLogic data monopoly |
| Private lending rate transparency | Dead | Same as matching platform with different skin |
| Tenant risk scoring (CDR-powered) | Dead | Equifax already does it, state regulations may block CDR consent, 30-67% consent failure rate, discrimination risk, advocacy backlash |
| SME lending / CDR credit scoring | Dead | MYOB/Xero/Equifax/Prospa all in the space |
| BNPL compliance tools | Conflict | Zihao works at Block (owns Afterpay) |

## What the Research Actually Revealed

### The Big Numbers (Fraud)
- CBA found **A$1 billion in suspected AI-assisted fraudulent home loans** (Feb 2026)
- Digital document forgeries up **244% YoY** in 2024
- Insurance fraud costs **A$2.2 billion/year**
- Identity fraud: **255,100 Australians** affected in 2023-24, costing A$1.6-3.1B/year
- Card fraud hit **A$913 million** in 2024 (up 20%)
- GST refund fraud (Operation Protego): **A$2 billion**, 57,000+ people
- Phoenix company fraud: **A$4.89-5.1 billion/year**
- Total annual fraud cost across all categories: **A$12-15 billion+**

### Key Australian Fraud Detection Players
- **Fortiro**: Lending document verification. 100+ checks in 30 seconds. Already in market
- **IDVerse/OCR Labs**: Identity verification. 300+ checks. Sydney-based
- **GBG/greenID**: Largest DVS gateway. 400+ clients
- **ICA/Shift Technology**: Building national insurance fraud platform (2026)

### Regulatory Tailwinds for Fraud Detection
- **Scams Prevention Framework**: Banks face A$50M fines for inadequate fraud prevention (June 2026)
- **Digital ID Act 2024**: ConnectID, myGovID expanding
- **CDR expansion**: Non-bank lenders July 2026

## Honest Conclusion

**The "AI + Australian finance" space is either too small, too crowded, or both.** Every direction we explored was either already being done by an incumbent or didn't have a large enough market.

The one exception where fraud is genuinely massive (A$12-15B/year) and growing fast (244% YoY for fake documents) — but even there, Fortiro exists for lending, IDVerse exists for identity, and Shift Technology is building an insurance fraud platform.

## What Might Still Work (Small Scale)

### Option 1: Fake Document Detector (Micro-SaaS)

**Not a company. A tool.**

```
fakechecker.com.au

Upload payslip / bank statement / tax return
    → AI checks: metadata, fonts, pixel analysis, format consistency
    → Cross-reference with known templates (ATO forms, major bank formats, major employer payslips)
    → 30 seconds → result: genuine / suspicious / likely fake
    → A$5-10 per check
```

**Why this might work despite Fortiro:**
- Fortiro is enterprise/lending focused (integration heavy, expensive)
- This is self-serve, pay-per-use, anyone can use it
- Target: mortgage brokers (15,000+), PM agents (10,000+), employers doing hiring, small lenders
- No integration needed — just upload a file on a website
- MVP: 2-3 weekends using Claude/GPT Vision + PDF metadata analysis + heuristics

**Why this might NOT work:**
- Hard to prove value (how does the customer know the result is correct?)
- Per-document revenue is tiny (need massive volume for meaningful income)
- Fortiro or Equifax could easily add a self-serve tier

**Realistic revenue:** If 500 users do 10 checks/month at A$8 = A$40K/month. Possible but requires significant marketing.

### Option 2: Consulting / Fractional CTO

**Not a product. A service.**

- You have Block-level credit/fraud ML experience. This is rare in Australia
- Australian fintechs (Prospa, Beforepay, Zip, small lenders) need this expertise but can't afford a full-time Block-level ML engineer
- Charge A$250-400/hour, work 10 hours/week on the side
- No product to build, no market to find — just sell your time and expertise
- Can evolve into a product if you spot a gap while consulting

**Realistic revenue:** 10 hrs/week × A$300/hr × 48 weeks = A$144K/year side income.

### Option 3: Do Nothing (Seriously)

You have a great job at Block. Your friend has a great job at Wagetap. Your wife's real estate investments are working.

Not every skill combination needs to become a startup. Sometimes the best "startup" is:
- Keep the high-paying job
- Invest in property (wife's expertise)
- Build savings
- Wait for a genuine insight that comes from being in the industry, not from research

The best startups come from **personal frustration** ("I had this problem and nobody solved it"), not from market research ("the TAM is $X billion"). If you haven't personally felt a burning pain point, forcing one through research rarely works.

## Summary

After 10+ documents of research covering private lending, tenant screening, SME credit, BNPL, fraud detection, and consumer finance in Australia:

**The Australian market is small.** 26 million people. Most niches are either too small to support a startup or already served by incumbents (Equifax, CoreLogic, MYOB/Xero, the Big 4 banks).

**Your skills are valuable.** But they might be most valuable inside a large company (Block) rather than as an indie startup in Australia.

**If you must build something:**
1. Start with the fake document detector (smallest, fastest to validate)
2. Or do consulting (zero risk, immediate revenue)
3. Use either as a way to stay close to the market and wait for a real insight

**The one thing NOT to do:** Quit your job to pursue any of these directions based on market research alone.
