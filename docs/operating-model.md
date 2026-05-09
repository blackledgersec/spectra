# SPECTRA Operating Model

## Delivery Model

SPECTRA is designed as an operator-guided methodology. The orchestration engine automates reconnaissance, classification, payload generation, and execution, but the operator retains control over critical decisions: scope boundaries, safety gate responses, chain escalation approval, and final severity ratings.

## Engagement Lifecycle

### Pre-Engagement

1. Scope definition with the client (which AI systems, which environments, what's in/out of bounds)
2. Rules of engagement — prohibited techniques, data handling requirements, escalation contacts
3. Evidence handling plan — how test data is stored, retained, and destroyed
4. Access provisioning — test accounts, API credentials, network access

### During Engagement

The pipeline runs iteratively. The operator may:

- Adjust payload generation based on early findings
- Escalate or de-escalate based on defensive profile results
- Pause execution when safety gates trigger
- Manually explore attack chain branches the automation didn't attempt
- Re-run specific stages after the target's behavior changes

### Post-Engagement

1. Finding validation — confirm each finding is reproducible and accurately described
2. Chain verification — walk each attack chain end-to-end
3. Remediation mapping — specific, actionable fixes for each finding
4. Report delivery — executive summary + technical findings + framework mapping
5. Debrief — lessons learned feed back into the knowledge base

## Compute Architecture

SPECTRA uses a hybrid compute model:

- **Local processing**: Reconnaissance, fingerprinting, payload generation, safety gates, and evidence storage all run locally. No engagement data leaves the operator's machine without explicit redaction.
- **Frontier API** (optional): For adaptive multi-turn strategy and executive summary generation, redacted context can be sent to a frontier model. The redaction proxy strips all PII, credentials, org names, and sensitive data before transmission.
- **Local models** (optional): For environments where no external API calls are permitted, local models handle all reasoning tasks with reduced capability.

## Safety Architecture

### Data Boundaries

The redaction proxy enforces a strict boundary between engagement data and any external service. Categories that are never transmitted externally include: person names, email addresses, phone numbers, SSNs, credit card numbers, API keys, database connection strings, internal URLs, organization names, IP addresses, PHI identifiers, passwords, file paths, and raw customer records.

### Operator Gates

Certain actions always require operator approval:

- Responding to REAL_SUSPECTED safety classifications
- Executing financial tool actions (any dollar amount)
- Escalating chain testing beyond the original scope
- Sending any data to external APIs for the first time in an engagement

## Adapter Architecture

The pipeline connects to targets through a pluggable adapter layer that abstracts the communication protocol. This allows testing AI systems regardless of their deployment model — direct API, web interface, embedded chat, or messaging platform integration.
