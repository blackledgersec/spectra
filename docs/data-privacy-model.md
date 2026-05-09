# SPECTRA Data Privacy Model

## Principle

Engagement data stays local. The operator's machine is the trust boundary. Any data that crosses that boundary is redacted first and audited.

## Redaction Proxy Architecture

The redaction proxy sits between the local pipeline and any external service (frontier API, cloud logging, etc). It enforces a strict allow/block classification on every piece of data.

### Blocked Categories (Never Transmitted Externally)

| Category | Detection Method |
|---|---|
| Person names | Named entity recognition |
| Email addresses | Regex pattern matching |
| Phone numbers | Regex pattern matching |
| SSN / Tax IDs | Regex + format validation |
| Credit card numbers | Regex + Luhn check |
| API keys and tokens | Pattern library (AWS, Azure, GCP, OpenAI, etc) |
| Database connection strings | Regex |
| Internal URLs and endpoints | URL pattern matching |
| Organization name | Exact match (configured per engagement) |
| Internal IP addresses | RFC 1918 range matching |
| PHI identifiers (MRN, DOB) | NER + regex |
| Passwords and secrets | Entropy analysis + pattern matching |
| File paths | Regex |
| Raw customer records | Structural analysis |

Each blocked item is replaced with a tagged placeholder (e.g., `[PERSON_1]`, `[EMAIL]`, `[API_KEY]`) that preserves the structure of the text without exposing the value.

### Allowed Categories (May Be Transmitted)

- NAICS sector classification
- Defensive profile classification (1-5)
- Behavioral profile summary (authority-responsive, fatigue-susceptible, etc)
- Attack category names
- Success/failure status
- Generic tool type names (CRM, email, database)
- Generic data type categories (regulated patient data, financial records)
- Chain template references
- Quantitative metrics (success rates, extraction rates)
- Evasion technique names

### Processing Pipeline

1. Regex pass — strip emails, SSNs, credit cards, URLs, IPs, API keys, connection strings, file paths
2. NER pass — strip person names, org names, locations, PHI identifiers
3. Org name replacement — exact match for configured target org and aliases
4. Entropy check — flag remaining high-entropy strings
5. Validation — confirm redacted text is still coherent
6. Audit log — write pre/post redaction to local-only audit log

### Operator Oversight

- Before the first external API call, the operator reviews 5 sample redacted prompts and signs off
- Every API-bound prompt is logged with pre/post redaction text
- Any redaction failure triggers an alert and pauses API calls
- The operator can review the audit log at any time

## Local-Only Mode

For clients that prohibit any external API usage, the pipeline runs entirely locally. All frontier API calls are disabled. The engagement report notes that frontier reasoning was not used, and the operator manually performs tasks that would have been delegated.

## Evidence Handling

- All engagement evidence is stored locally on the operator's machine
- Evidence at rest is encrypted
- Findings document data categories exposed but do not reproduce actual data values
- Evidence retention follows the engagement's evidence handling plan
- Client notification follows the rules of engagement
