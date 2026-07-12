# Govtech

## Scope
Government and civic technology: citizen services, permitting, benefits administration, voting systems, and digital transformation of public sector.

## Core principles
- Public process is accountable: every decision must be traceable, transparent, and appealable; opaque algorithms used in welfare decisions or criminal justice face legal challenges.
- Legacy systems are entrenched: agencies run mainframes (COBOL), custom databases (30 years old), and paper processes; integration is painful and disruptive replacement is risky.
- Equity is non-negotiable: government serves all citizens, including those without smartphones or broadband; accessibility and language access are mandatory, not nice-to-have.
- Citizen data is sensitive: SSN, income, health, location; FERPA, HIPAA, and state laws apply; data breaches destroy trust in government.
- Adoption is slow but sticky: once a citizen uses e-filing, they expect it; once a business gets digital permits, manual processes are unacceptable; incentives shift gradually but permanently.

## Apex practices
- Design for digital literacy (ages 8–88, non-native speakers): plain language, step-by-step workflows, error messages that explain what went wrong and how to fix it.
- Integrate with legacy systems via APIs or middleware (ESBs: Enterprise Service Buses); direct database access or file transfer is fragile and unmaintainable.
- Implement audit trails and decision logging: why was the benefit denied? What was the calculation? Citizens must be able to appeal based on evidence.
- Plan for procurement and compliance: government contracts have lead times (RFP, evaluation) and compliance (ADA, Section 508 accessibility, FIPS encryption standards).

## Pitfalls
- Assuming internet access; provide offline options (in-person, phone, mail) or face equity complaints and low adoption.
- Ignoring legacy data; migrating 50 years of records from paper/mainframe is harder than rebuilding from scratch, so it becomes a blocker.
- Over-automating decisions (welfare denials, benefit eligibility) without human review; algorithmic bias leads to systematic harm and political backlash.

## Tools & references
USWDS (US Web Design System, accessible components), 18F (federal design agency), state procurement portals, accessibility standards (Section 508, WCAG 2.1 AA), case management systems (Salesforce, specialized GovTech SaaS).
