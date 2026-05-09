# SPECTRA Framework Alignment

## Overview

SPECTRA findings map to four major security and AI governance frameworks. This alignment ensures that assessment results speak the language of compliance teams, risk managers, and auditors — not just security engineers.

## OWASP LLM Top 10 (2025)

| OWASP ID | Risk | SPECTRA Coverage |
|---|---|---|
| LLM01 | Prompt Injection | Direct and indirect injection across all payload categories |
| LLM02 | Sensitive Information Disclosure | System prompt extraction, cross-context data leakage, RAG data exfiltration |
| LLM03 | Supply Chain Vulnerabilities | Tool integration abuse, MCP security testing |
| LLM04 | Data and Model Poisoning | Knowledge base poisoning, memory persistence attacks, RAG index manipulation |
| LLM05 | Improper Output Handling | Output weaponization, downstream injection via tool outputs |
| LLM06 | Excessive Agency | Unauthorized action execution, tool abuse chains, scope escalation |
| LLM07 | System Prompt Leakage | 7-technique graduated extraction methodology |
| LLM08 | Vector and Embedding Weaknesses | Vector store poisoning, retrieval manipulation |
| LLM09 | Misinformation | Output manipulation, belief injection, knowledge base corruption |
| LLM10 | Unbounded Consumption | Resource abuse, token exhaustion, recursive prompt attacks |

## MITRE ATLAS

SPECTRA maps to ATLAS techniques across the attack lifecycle:

- **Reconnaissance**: AML.T0002 (Active Scanning), AML.T0012 (Valid Accounts)
- **Initial Access**: AML.T0051 (LLM Prompt Injection), AML.T0049 (Exploit Public-Facing Application)
- **Execution**: AML.T0040 (ML Model Inference API Access), AML.T0043 (LLM Plugin Compromise)
- **Persistence**: AML.T0020 (Poison Training Data), AML.T0019 (Publish Poisoned Datasets)
- **Impact**: AML.T0048 (Denial of ML Service), AML.T0024 (Evade ML Model)

## NIST AI RMF

| Function | SPECTRA Contribution |
|---|---|
| GOVERN | Tests whether AI governance policies are enforced at the technical level |
| MAP | Maps the actual attack surface of deployed AI systems against stated boundaries |
| MEASURE | Quantifies risk through extraction rates, success rates, and scope estimation |
| MANAGE | Produces specific remediation recommendations with implementation priority |

## ISO 42001

SPECTRA findings map to ISO 42001 Annex A controls for AI management systems, supporting organizations pursuing or maintaining certification. Assessment reports include control-level mapping for each finding.

## Why Multi-Framework Mapping Matters

Different stakeholders consume different frameworks:

- **CISOs and security teams** → OWASP LLM Top 10, MITRE ATLAS
- **Risk and compliance teams** → NIST AI RMF, ISO 42001
- **Boards and executives** → Business impact narratives derived from chain analysis
- **Engineering teams** → Specific technical remediation from each finding

SPECTRA's reporting layer produces all of these views from the same underlying finding data.
