# 5. Regulatory Framework

## Overview

Australian private lending regulation centers on the distinction between **consumer** and **commercial** lending. Consumer lending is heavily regulated; commercial lending is largely exempt.

## NCCP Act (National Consumer Credit Protection Act 2009)

The primary federal legislation governing consumer credit, administered by **ASIC**.

### When NCC Applies (all must be true):
1. Borrower is a **natural person** or strata corporation
2. Credit is for **personal, domestic, household purposes** OR to purchase/renovate **residential investment property**
3. A **charge** is made for the credit
4. Credit provider provides credit **in the course of business**

### Key Exemptions:
- **Business/commercial purpose loans** — the main exemption private lenders use
- **Company borrowers** — loans to companies (not natural persons)
- **Short-term credit** — contracts ≤62 days (unless fees >5% or interest >24% p.a.)
- **Small business lending exemption** — extended to **3 October 2026** (exempts from responsible lending obligations)

### Responsible Lending Obligations (RLOs):
For regulated loans under RG 209:
- Make **reasonable inquiries** about borrower's financial situation
- Take **reasonable steps to verify** financial situation
- Assess that contract is **"not unsuitable"** for the consumer

## Australian Credit Licence (ACL)

### You NEED an ACL if you:
- Provide credit to natural persons for personal/domestic/household purposes
- Provide credit for residential investment property
- Act as a mortgage broker for regulated credit

### You DO NOT need an ACL if you:
- Lend exclusively for business/commercial purposes
- Lend only to corporate entities
- Only provide **background technology** (SaaS) to licensed entities

### ACL Requirements:
- Application fee: A$2,055-$4,624
- Responsible Managers with Certificate IV + 2 years experience
- Professional indemnity insurance
- Membership in AFCA (external dispute resolution)
- Compliance systems and adequate financial resources
- ASIC targets 150-day decision timeline

## Commercial Purpose Declaration

The primary mechanism private lenders use to operate outside NCCP:

- Borrower signs declaration stating credit is predominantly for **business/investment purposes**
- Form must follow **Regulation 68** prescribed format
- Must contain a warning about losing NCC protections
- Lender must not know the loan is actually for personal purposes

### ASIC Scrutiny:
- ASIC is actively targeting misuse of commercial purpose declarations
- **ASIC v Oak Capital**: Proceedings for unconscionable conduct against private lender that coerced consumers into signing declarations
- ASIC "will not hesitate to intervene where progress falls short"

## ASIC Regulatory Actions (2024-2025)

- **ASIC Report 814** (Sept 2025): Surveyed 28 private credit funds. Flagged opaque fees, related-party transactions, inconsistent valuations, governance weaknesses
- **Interim stop orders** on three La Trobe products
- **Stop orders** against RELI Capital Mortgage Fund
- **Dedicated Private Credit Institutional Loan Market Unit** established mid-2024

## Australian Financial Services Licence (AFSL)

Separate from ACL. Required for:
- Operating a **managed investment scheme** (including private credit funds)
- Providing financial advice
- Dealing in financial products

Most private credit funds need **both AFSL and ACL**.

## For SaaS/Fintech Startups

### Do you need a licence?
- **Pure B2B SaaS** (software to licensed lenders): Generally **NO** licence needed
- **Platform touching consumers**: Likely need ACL and/or AFSL
- **Marketplace pooling investor money**: Need AFSL (managed investment scheme)

### Starting options:
- **Credit representative**: Operate under another entity's ACL (lower barrier)
- **Enhanced Regulatory Sandbox**: Test without licence for up to 24 months
- **ASIC Innovation Hub**: Free guidance (innovationhub@asic.gov.au)

## AML/CTF (Anti-Money Laundering)

Regulated by **AUSTRAC** under AML/CTF Act 2006.

### Requirements for lenders:
1. Enrol with AUSTRAC
2. Develop AML/CTF program (risk-based approach)
3. Customer identification (KYC) before providing services
4. Ongoing customer due diligence
5. Report suspicious matters, threshold transactions ($10K+ cash)
6. Record keeping for 7 years

### 2024-2025 Reforms:
- **Tranche 2 expansion** from **1 July 2026**: Extends to real estate agents, lawyers, accountants
- New AML/CTF Rules 2025 with outcomes-focused approach
- Enrolment for Tranche 2 entities opens 31 March 2026

## Privacy Act 1988

### Key points for lending:
- Credit providers captured **regardless of turnover** (unlike general A$3M threshold)
- 13 Australian Privacy Principles (APPs) govern data handling
- **Notifiable Data Breaches**: Must notify OAIC + affected individuals within 30 days
- 2024 penalty reform: Up to **A$50M**, 3x benefit, or **30% of adjusted turnover**

### Cross-border data (APP 8):
- Must ensure overseas recipients comply with APPs
- New certification mechanism for whitelisted countries (from 2025)
- Relevant if using AWS/Azure/GCP in international regions

### Recommended certifications:
1. **SOC 2 Type 2** — most requested by enterprise B2B clients
2. **ISO 27001** — APAC market credibility
3. **CDR Schedule 2** — if becoming Accredited Data Recipient
4. **PCI DSS** — if handling payment card data

## Consumer Data Right (CDR) / Open Banking

### Current status:
- Live for banking since July 2020
- 96 Data Holders active, 135+ CDR Representatives
- **Expanding to non-bank lenders from July 2026** (Version 8 Rules)

### Key timeline:
| Date | Milestone |
|------|-----------|
| July 2020 | CDR live for banking |
| Aug 2024 | Action Initiation ("write access") passed into law |
| July 13, 2026 | Non-bank product data sharing |
| Nov 9, 2026 | Non-bank consumer data sharing begins |
| Sep 13, 2027 | Full non-bank consumer data sharing |

### Action Initiation (game-changer):
Enables consumers to instruct accredited parties to:
- Make payments on their behalf
- Open/close accounts
- Switch providers
- Set up direct debits

### How to access CDR data:
1. **Full ADR accreditation**: Direct access, high compliance burden
2. **Sponsored (Affiliate)**: Operate under an existing ADR
3. **CDR Representative**: Lightest option, operate under ADR's accreditation
4. **Use intermediary**: Frollo, Basiq, or Yodlee (they hold ADR accreditation)

### CDR data available for lending:
- Customer information (name, contact, ABN)
- Account details (balances, direct debits, scheduled payments)
- Transactions (date, amount, categorization)
- Product information (fees, rates, features)

---

Sources:
- [NCCP Act - Federal Register of Legislation](https://www.legislation.gov.au/C2009A00134/latest)
- [ASIC - Credit Licensees](https://www.asic.gov.au/for-finance-professionals/credit-licensees/)
- [ASIC - Innovation Hub](https://www.asic.gov.au/for-business-and-companies/innovation-hub/)
- [AUSTRAC - AML/CTF Reform](https://www.austrac.gov.au/amlctf-reform)
- [OAIC - Australian Privacy Principles](https://www.oaic.gov.au/privacy/australian-privacy-principles)
- [CDR Official Website](https://www.cdr.gov.au/)
- [Ashurst - CDR Action Initiation](https://www.ashurst.com/en/insights/action-initiation-under-australia-consumer-data-right-becomes-law/)
- [Treasury - Small Business RLO Exemption](https://treasury.gov.au/consultation/c2024-558382)
