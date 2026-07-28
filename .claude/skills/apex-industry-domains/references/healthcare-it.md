# Healthcare IT

## Scope
Clinical and administrative systems for patient care, billing, and health records: interoperability standards (HL7, FHIR), compliance (HIPAA, GDPR), and patient safety as non-negotiable.

## Core principles
- Patient safety is existential: a bug can kill someone; all changes require traceability, testing, and validation. This shapes the entire development cycle (slower, more careful, auditable).
- Data privacy (HIPAA, GDPR, state laws) means patient information is never logged, cached, or exposed; encryption, access controls, and audit trails are architecture requirements, not features.
- Interoperability is critical but fragmented: HL7v2 (legacy, text-based), HL7v3 (XML), and FHIR (modern REST/JSON) coexist; integrations with EHRs, labs, pharmacies must translate between standards.
- Compliance audits are scheduled (annually or per regulation); systems must demonstrate security, data handling, and disaster recovery through logs and configurations — design for auditability.
- Clinical workflows are non-negotiable: a system can't impose a workflow that contradicts how clinicians work; understand the clinic first, design the system second.

## Apex practices
- Treat uptime as non-negotiable (99.9% SLA typical); distributed databases with replication, load balancing, and failover are standard infrastructure.
- Use role-based access control (RBAC) with audit trails: every access to sensitive data is logged (who, what, when, why); exceptions require explicit approval and documentation.
- Integrate with HL7/FHIR standards early; custom data formats fragment the ecosystem and make future interops expensive.
- Implement end-to-end encryption for data in transit and at rest; key management and rotation are operational requirements.

## Pitfalls
- Assuming privacy can be added later; it must be baked into architecture from day one.
- Handling HIPAA as purely compliance rather than as embedded in engineering (logging what shouldn't be logged, caching sensitive data).
- Integrating with legacy EHRs without understanding their data model and limitations; many are decades old and fragile.

## Tools & references
HL7 FHIR spec, HIPAA Privacy Rule (45 CFR 164), GDPR Article 32 (security), EHRs (Epic, Cerner, Athena), cloud healthcare (AWS HIPAA, Azure, GCP Compliance), patient safety reporting (ECRI, ISMP).
