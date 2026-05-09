# Sample Remediation Map

This is a sanitized example of a SPECTRA remediation map produced by the reporting stage.

## Remediation Priority Matrix

| Finding | Severity | Primary Mitigation | Implementation Effort | Business Risk Reduction |
|---|---|---|---|---|
| Cross-patient data access | Critical | Delegated authorization + pre-retrieval ACL | Medium-High | Eliminates the primary breach vector |
| System prompt extraction | High | Prompt hardening + output filtering | Low | Prevents information disclosure that enables targeted attacks |
| Guardrail bypass via authority claim | High | Instruction hierarchy enforcement | Low-Medium | Closes the most common social engineering vector |
| Tool over-permissioning | Medium | Principle of least privilege on service accounts | Medium | Reduces blast radius of any successful injection |
| Behavioral fatigue at turn 8 | Medium | Multi-turn conversation limits + reset mechanisms | Low | Prevents gradual erosion of safety controls |

## Recommended Implementation Order

### Phase 1: Immediate (Week 1-2)

**Delegated authorization**: Replace conversational authorization (where the AI system trusts role claims in the conversation) with delegated authorization (where the AI system verifies roles against the identity provider). This is the highest-impact single fix because it breaks the entry point for the most severe attack chain.

### Phase 2: Short-term (Week 3-4)

**Pre-retrieval access control**: Add patient-provider relationship checks before the AI system retrieves patient data, not after. Post-retrieval filtering (the current model) means the data has already been loaded into the model's context, creating extraction opportunities even if the output filter blocks the direct response.

**Prompt hardening**: Restructure the system prompt to use explicit instruction hierarchy. The system prompt should include directives that cannot be overridden by user input, regardless of claimed authority.

### Phase 3: Medium-term (Month 2)

**Service account scoping**: Reduce the AI system's backend service account permissions to the minimum required. Currently, the service account can access all patient records regardless of which user is authenticated. Scope it to the authenticated user's authorized patient list.

**Conversation session limits**: Implement maximum conversation length and periodic re-authentication to prevent behavioral fatigue exploitation.

### Phase 4: Ongoing

**Monitoring and anomaly detection**: Deploy logging that flags unusual data access patterns (bulk lookups, sequential ID enumeration, cross-department queries) and alerts the security team.

## Retest Guidance

After remediation, SPECTRA recommends a targeted retest focused on:

1. Re-running the cross-patient access chain to verify delegated auth breaks the chain at step 1
2. Re-running authority escalation payloads to verify instruction hierarchy holds
3. Re-running system prompt extraction techniques to verify output filtering catches new vectors
4. Testing for bypass paths around the new controls (e.g., can the authority claim be structured differently to evade the new checks?)

---

*This example demonstrates the structure of a SPECTRA remediation map. All specific system names, configurations, and implementation details have been generalized.*
