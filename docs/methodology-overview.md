# SPECTRA Methodology Overview

## The 9-Stage Pipeline

SPECTRA organizes AI adversarial testing into a structured pipeline where each stage produces data that feeds downstream stages. This creates context-aware testing that adapts to the specific target rather than running generic payloads.

### Stage 0: Engagement Setup

Define the rules of engagement, target connection parameters, scope boundaries, and safety protocols. Establish evidence handling procedures and operator authorization levels.

### Stage 1: Target Connection

Establish and validate the connection to the target AI system. Verify the communication channel, confirm authentication, and perform initial health checks.

### Stage 2–3: Reconnaissance and Capability Discovery

Systematically enumerate the target's capabilities, restrictions, connected systems, data sources, and behavioral characteristics through a 5-phase methodology:

1. **Conversational Enumeration** — Discover what the system can do through natural interaction
2. **System Prompt Extraction** — Attempt to recover the system's configuration using graduated techniques
3. **API and Integration Mapping** — Identify connected tools, APIs, and external services
4. **Data Source Profiling** — Map data access patterns, sensitivity levels, and access controls
5. **Behavioral Fingerprinting** — Characterize the system's response patterns to authority, fatigue, and social engineering

### Stage 4: System Classification and Context Mapping

Classify the target by industry sector (NAICS code) and load the corresponding regulatory requirements, data sensitivity hierarchy, and domain-specific terminology. This stage turns generic testing into context-aware testing.

Classification uses weighted signal matching against sector indicators discovered during reconnaissance. Confidence scoring determines whether the classification is automatic (≥0.80), operator-assisted (0.50–0.79), or manual (<0.50).

### Stage 5: Defense Fingerprinting

Profile the target's defensive posture by probing five defensive layers and classifying the result into one of five profiles:

| Profile | Name | Characteristics |
|---|---|---|
| 1 | Minimal | No input/output filtering, soft guardrails, conversational auth |
| 2 | Input Filtered | Keyword or semantic input filtering, no output controls |
| 3 | Layered Defenses | Input filtering + output filtering (PII masking, content blocking) |
| 4 | Gateway Protected | External AI gateway (rate limiting, policy enforcement) |
| 5 | Architecturally Hardened | Delegated auth + pre-retrieval ACL + human-in-the-loop gates |

The defensive profile directly informs which evasion strategies are applicable and which attack categories are most likely to succeed.

### Stage 6: Test Generation (Payload Creation)

Generate context-aware test payloads using the target profile, sector classification, and defensive profile as inputs. Payloads are organized by outcome category and paired with applicable evasion strategies.

Quality validation ensures generated payloads are realistic (would a real user in this industry plausibly send this?), non-duplicative, and within scope.

### Stage 7: Execution (Payload Delivery + Safety Gates)

Deliver payloads to the target with active safety controls:

- **Safety Gate**: Every response is classified into safety tiers (SAFE, SYNTHETIC, REAL_SUSPECTED, REAL_CONFIRMED). Real data triggers automatic pauses and operator alerts.
- **Redaction Proxy**: Sensitive data in responses is redacted before logging or external API transmission.
- **Outcome Assessment**: Each response is evaluated for success indicators specific to the payload's outcome category.

### Stage 8: Attack Chain Composition

Successful findings are composed into multi-step attack chains that demonstrate real business impact. Each chain maps an entry point through escalation to a quantifiable outcome.

Chain composition checks preconditions between findings — if Finding A's output satisfies Finding B's entry requirement, they compose into a chain with escalated severity.

### Stage 9: Report Generation

Produce structured findings with severity ratings, framework mappings, remediation recommendations, and an executive summary. Each finding includes the full attack chain, business impact analysis, and specific mitigation guidance.

## Key Differentiators

- **Context-aware**: Every payload reflects the target's actual industry, regulatory environment, and connected systems
- **Safety-first**: Active safety gates prevent uncontrolled data exposure during testing
- **Framework-mapped**: Findings map to OWASP, MITRE ATLAS, NIST AI RMF, and ISO 42001
- **Chain-oriented**: Individual findings are composed into business-impact attack chains, not isolated vulnerabilities
- **Sector-specific**: Industry knowledge bases provide domain terminology, regulatory requirements, and data sensitivity hierarchies
