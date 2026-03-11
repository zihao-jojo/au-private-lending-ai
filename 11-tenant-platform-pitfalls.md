# 11. Tenant Risk Platform: Deep Research on Pitfalls

## TL;DR — The Idea Has Serious Problems

After deep research, the CDR-powered tenant screening opportunity is **much harder than it looked**. There are 5 near-fatal issues:

1. **Equifax is already doing it** (CDR-powered tenant affordability check via Basiq)
2. **State regulations may block it** (VIC prescribed forms from March 2026)
3. **CDR consent fails 30-67% of the time** (tenants can't complete the flow)
4. **Discrimination risk from bank transaction data** (gambling = disability, payday loans = protected groups)
5. **Tenant advocacy groups will attack** ("social credit scoring for renters" writes itself)

---

## Pitfall 1: Equifax Is Already Here

This was the biggest surprise. **Equifax already offers a "Tenant Affordability Check" that uses CDR bank transaction data via Basiq.**

- Automated retrieval of bank transactions from **70+ financial institutions**
- Analyses 90 days of data (option for up to 2 years)
- Sorts expenses, identifies income, verifies rental payment history
- Uses **Basiq technology** under the hood
- Already integrated with platforms like Cubbi

Additionally, Equifax launched **"Open Score"** with Mastercard — a CDR-consented financial health score designed for real-time assessment.

**What this means:** We are NOT entering a greenfield market. The dominant credit bureau in Australia already has a CDR-powered tenant screening product. They have the brand, the data, the integrations, and the regulatory infrastructure.

The question becomes: can we build something meaningfully better than what Equifax already has? Maybe (their product is likely basic/enterprise-y), but "slightly better Equifax" is not a compelling startup thesis.

---

## Pitfall 2: State Regulation Is Closing In Fast

Every major state is introducing **prescribed rental application forms** that limit what information landlords can request:

| State | Regulation | Date | Impact |
|-------|-----------|------|--------|
| **Victoria** | Form 3A — mandatory prescribed application form. **Cannot request ANY information outside the form** | 31 March 2026 | If CDR consent is not on Form 3A, it may be **illegal** to ask tenants to complete it |
| **Queensland** | Form 22/R22 — prescribed form. Must offer non-digital submission option. Cannot force third-party platforms | 1 May 2025 | CDR consent must be optional, reducing adoption |
| **South Australia** | Form A1 — max 2 documents per category (identity, financial, suitability). Prohibited info list | 1 Jan 2026 | CDR output may count as one of only 2 allowed financial documents |
| **NSW** | Standardised application form. Limits on data collection. No charging tenants for checks | 31 March 2026 | CDR consent mechanism may not be accommodated |

**Victoria is the critical risk.** "Must not request any information outside the prescribed form" could make CDR consent **illegal in VIC** if the form doesn't include it. VIC is Australia's second-largest rental market.

---

## Pitfall 3: CDR Consent Is Broken

The practical reality of CDR consent in Australia:

- **67% of Frollo users** had an unsuccessful first attempt at CDR consent
- Some users tried **up to 5 times** before giving up
- **30% of consent authorizations are failing** at banks
- **88% of failures** are due to login issues, OTP problems, or bank-side technical errors
- CDR consent **expires annually** and extension doesn't work properly
- More than **50%** of data sharing arrangements were discontinued or lapsed in 2023
- Only **0.31%** of bank customers had active CDR sharing in late 2023 (~530K by H2 2024)

**In a rental application context:** Tenants are stressed, applying for 10-20 properties simultaneously, competing with 30+ other applicants. Any friction = they skip your consent flow and submit a regular application instead.

If 30-67% of tenants fail the CDR consent flow, your product only works for 33-70% of applicants. That makes it unreliable for agents.

---

## Pitfall 4: Discrimination Risk Is Severe

CDR bank transaction data contains signals that proxy for **protected attributes** under Australian anti-discrimination law:

| Transaction Type | What It Reveals | Discrimination Risk |
|-----------------|-----------------|-------------------|
| Gambling (TAB, Sportsbet, Crown) | Gambling behavior | **Disability discrimination** — gambling addiction is a recognized mental health condition |
| Payday loans (Wagetap, Beforepay) | Financial stress | Disproportionately affects **Indigenous Australians, single parents, people with disabilities** |
| Religious institutions (mosques, churches, temples) | Religion | **Religious discrimination** |
| Health providers (psychologists, fertility clinics, gender clinics) | Health conditions | **Disability/sex discrimination** |
| Alcohol/substance purchases | Consumption habits | Potentially discriminatory |
| Political donations | Political affiliation | **Political belief discrimination** |

Even if the algorithm doesn't explicitly use these categories:
- **Indirect discrimination**: If the model produces worse scores for protected groups (statistically correlated with spending patterns), you face legal liability
- **Proxy discrimination**: Income stability, savings levels, and spending patterns all correlate with race, age, disability, and family status

**There is no safe way to use raw CDR transaction data for tenant scoring without touching discriminatory signals.** Even "sanitized" categories still proxy for protected attributes.

---

## Pitfall 5: Tenant Advocacy Will Attack

This is not hypothetical. Active campaigns are already happening:

- **CHOICE** published a major investigation finding RentTech platforms collect excessive data and use "black box AI" to evaluate applicants. 41% of renters felt pressured to use third-party platforms
- **AHURI** research found digitization has outpaced legal frameworks, creating "potential gaps in privacy protection"
- Academic researchers characterize algorithmic tenant screening as **"automated landlordism"** reinforcing power imbalances
- **Tenants' Union NSW**, **Tenants Victoria**, and **Tenants Queensland** are all actively campaigning on data privacy
- CHOICE forced **TICA to delete data** after finding illegal data retention — they will do the same to any new player
- From **October 2024**, charging renters for background checks is banned

**The "social credit scoring" narrative:** Any product generating a numerical score from bank spending data will be compared to social credit scoring. Conspiracy-adjacent communities have already linked Digital ID + rental data to these narratives. A single negative media story could be fatal.

---

## Pitfall 6: Government Is Already Building This

The Australian Government is **piloting CDR + Digital ID for rental applications**:

- Multiple consortia selected, including **CBA, Ailo, and PropertyMe**
- **ConnectID** selected for identity verification in 3 of 4 pilots
- Government is defining how CDR data should be used in rental contexts
- If the government sets the rules, they may favor the incumbents (CBA, PropertyMe) who are in the pilot

**You would be building something the government and major banks are already piloting together.**

---

## Pitfall 7: Incoming Privacy Law Changes

From **10 December 2026** (Privacy and Other Legislation Amendment Act 2024):
- Mandatory disclosure of automated decision-making in privacy policies
- Expected **right to meaningful explanation** of algorithmic decisions
- Mandatory **privacy impact assessments** for high-risk activities
- Potential removal of the small business Privacy Act exemption

**Building an ML-powered tenant scoring system just as Australia introduces transparency requirements for automated decision-making is bad timing.**

---

## What the UK Experience Shows

UK has had Open Banking since 2018. Relevant tenant screening players:

| UK Company | What They Did | Lesson |
|-----------|--------------|--------|
| **Canopy** | RentPassport using Open Banking + Experian. Also DepositFree (deposit replacement) | **25% lost customers at bank connection step** before partnering with Plaid. Consent UX is the critical failure point |
| **CreditLadder** | Uses Open Banking to report rent payments to credit bureaus | **Pro-tenant framing** ("build your credit") avoids backlash vs "score tenants" |
| **Goodlord** | Open Banking for financial referencing | Position as "faster, less fraud" not "better scoring" |
| **Homeppl** | Open Banking + fraud detection + behavioral analysis | Claims to **approve MORE tenants** — inclusion narrative works better |

**Key insight: No UK player has built a dominant Open Banking tenant scoring business.** Even with 7+ years of mature Open Banking infrastructure, UK tenant screening is still primarily traditional referencing. Open Banking is a supplement, not a replacement.

**The most successful framing is pro-tenant ("build your credit", "get approved faster", "prove your worthiness"), NOT pro-landlord ("score and filter tenants").**

---

## Existing Competitive Landscape (More Crowded Than Expected)

| Player | What They Do | CDR/OB Data? | Notes |
|--------|-------------|-------------|-------|
| **TICA** | Blacklist (7M records). Dominant | No | Entrenched. $605/yr unlimited |
| **NTD (Equifax)** | Blacklist + credit data | No | Equifax-owned. $25/check |
| **Equifax Tenant Affordability** | **CDR bank data via Basiq** | **YES** | Already doing what we planned |
| **Equifax Open Score** | CDR financial health score | **YES** | With Mastercard |
| **Snug** | Digital application platform | No | IAG/Folklore backed. Integration partner? |
| **2Apply (IRE)** | Application + NTD integration | No | Widely used |
| **Ignite (REA Group)** | Application via realestate.com.au | No | REA controls massive application flow |
| **Cubbi** | Screening with ID verification + affordability | Uses Equifax/Basiq | Already CDR-adjacent |
| **Ailo** | PM platform, 200K users | CDR pilot participant | Government-backed |
| **RentBetter** | DIY landlord tools + NTD | No | Self-managing landlord market |

---

## Honest Assessment

### The thesis was:
> "Nobody is using CDR data for tenant screening. Wide open market."

### The reality is:
> "Equifax already does it. The government is piloting it. State regulations may block it. CDR consent is broken. Advocacy groups will attack it. The UK tried it and it didn't become a big business."

### What could still work (modified approach):

If we still want to operate in the rental/property space, the research suggests a different angle:

**1. Rent Credit Building (CreditLadder model)**
- Help tenants get credit for paying rent on time
- Use CDR to verify rent payments → report to credit bureaus
- Pro-tenant positioning avoids backlash
- But: CreditLadder exists and hasn't become huge

**2. Deposit Replacement Product**
- Tenants pay a small monthly fee instead of a 4-week bond
- Priced by risk score (CDR-powered internally, but tenant-facing product is "save money on your bond")
- Canopy does this in UK
- Lower discrimination risk (tenant chooses to use it)
- But: regulatory complexity, needs insurer partnership

**3. Tool for Property Managers (not scoring tenants)**
- Automate the admin of processing 30+ applications
- Extract and organize data from submitted documents
- Auto-check TICA/NTD
- Summarize and rank applications
- NOT a CDR consent product — just making agents' existing workflow faster
- Less sexy but more practical, fewer regulatory issues

**4. Accept the reality and move to a different market entirely**
- The team's skills (credit ML + CDR + property) may be better applied elsewhere
- SME cash flow intelligence
- Insurance fraud detection
- BNPL risk modeling
- These markets are larger and less politically sensitive than tenant screening

---

## Sources

- [Equifax Tenant Affordability Check](https://www.equifax.com.au/business-enterprise/products/tenant-affordability-check)
- [Equifax & Mastercard Open Score](https://www.openbankingexpo.com/news/equifax-australia-and-mastercard-launch-open-score-to-improve-financial-inclusion/)
- [CHOICE RentTech Investigation](https://www.choice.com.au/data-protection-and-privacy/data-collection-and-use/how-your-data-is-used/articles/choice-renttech-report-release)
- [CHOICE TICA Data Deletion](https://www.choice.com.au/consumers-and-data/data-collection-and-use/how-your-data-is-used/articles/tenant-database-operator-tica-forced-to-delete-renter-data)
- [Digital ID & CDR Rental Pilot](https://www.finance.gov.au/about-us/news/2025/digital-id-and-cdr-protecting-renters-personal-information)
- [PropertyMe CDR Pilot](https://www.propertyme.com.au/blog/propertyme/propertyme-selected-to-pilot-federal-government-led-initiative-to-protect-renters-information)
- [Victoria Rental Reforms](https://www.consumer.vic.gov.au/housing/renting/new-changes-to-the-rental-laws)
- [QLD Rental Law Changes](https://www.rta.qld.gov.au/rental-law-changes)
- [SA Rental Reforms](https://cbs.sa.gov.au/campaigns/rental-reforms)
- [NSW Rental Law Changes](https://www.nsw.gov.au/departments-and-agencies/fair-trading/news/changes-to-rental-laws)
- [Frollo CDR Consent Failure Rates](https://www.openbankingexpo.com/news/frollo-report-finds-growing-momentum-behind-open-banking-in-australia/)
- [97% of Banks Have CDR Data Issues](https://www.theadviser.com.au/tech/46559-97-of-banks-have-open-banking-data-issues-for-mortgages)
- [CDR Adoption 0.31%](https://www.fintechaustralia.org.au/newsroom/fintech-australia-unveils-2025-cdr-ecosystem-map-and-report)
- [AHURI Tenant Data Privacy](https://www.ahuri.edu.au/research/final-reports/454)
- [Automated Landlordism Research](https://www.tandfonline.com/doi/full/10.1080/02673037.2025.2453005)
- [Privacy Act Reform — ADM Transparency](https://legalvision.com.au/automated-decision-making-new-privacy-rules/)
- [Canopy UK + Plaid](https://plaid.com/customer-stories/canopy/)
- [CreditLadder UK](https://creditladder.co.uk/tenants)
- [Basiq Pricing ($0.39/user/month)](https://www.basiq.io/pricing.html)
- [TICA Pricing](https://www.tica.com.au/ten-check.php)
- [Snug - Tractor Ventures](https://www.tractorventures.com/post/snugs-two-pronged-approach-to-growth-and-transforming-property-sector)
