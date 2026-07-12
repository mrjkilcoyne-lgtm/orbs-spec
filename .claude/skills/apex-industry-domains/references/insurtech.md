# Insurtech

## Scope
Insurance technology: underwriting (risk assessment, pricing), claims processing, fraud detection, and policy management.

## Core principles
- Risk pooling is the model: many low-probability-high-cost events (car crashes, house fires, illness) are insurable via spreading cost across policyholders; actuaries price using historical claims data.
- Underwriting is risk assessment: data (age, location, health history, claims history, vehicle, lifestyle) predicts claim probability; models price accordingly; discrimination laws limit variables.
- Claims are expensive: processing, fraud investigation, and payout are costlier than premium if not controlled; automation (intake, validation, fraud scoring) reduces cost.
- Fraud is systematic: staged claims, exaggerated damages, and false reporting are common; detection requires pattern recognition (claims analytics, SIU: Special Investigation Unit).
- Regulation is heavy: state insurance commissions regulate pricing, disclosures, reserves, and solvency; changes require approval and proof of fairness (no discriminatory pricing).

## Apex practices
- Build underwriting models (logistic regression, gradient boosting) on historical claims data; models predict claim probability by risk profile.
- Implement fraud scoring: claims flagged for review based on unusual patterns (repeated small claims, claims just above deductible, policy timing before claim).
- Automate claims intake: OCR (optical character recognition) for documents, API for third-party data (police reports, medical records), structured forms reduce manual entry.
- Use telematics (IoT: sensors in vehicles or homes) for dynamic underwriting: driving behavior (acceleration, braking, time-of-day) and home conditions (security, maintenance) inform pricing.

## Pitfalls
- Over-relying on algorithmic pricing; if models encode discrimination (zip code as proxy for race, gender for health), regulators and plaintiffs sue.
- Assuming historical data represents future risk; climate change, new technologies, and social shifts alter risk profiles.
- Neglecting customer experience in claims processing; a frustrating claims experience kills retention even if claims are paid correctly.

## Tools & references
Actuarial science (Society of Actuaries), claims management (Guidewire, Duck Creek), fraud detection (SAS, IBM), pricing regulation (state commissioners), telematics (Metromile, DriveFactor).
