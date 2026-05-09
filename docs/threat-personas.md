# SPECTRA Threat Personas

## Why Threat Personas Matter for AI Testing

Traditional penetration testing uses generic attack scenarios. AI adversarial testing requires **context-aware threat modeling** because the attack surface changes based on who the attacker is, what they want, and how they interact with the system.

SPECTRA defines threat personas that drive payload generation. Each persona has different goals, access levels, and techniques — and each maps to different attack chains and business outcomes.

## Persona Framework

### External Attacker

An outsider with no legitimate access attempting to exploit the AI system through its public-facing interface.

- **Access level**: Public user, unauthenticated or self-registered
- **Primary goals**: Data exfiltration, system prompt extraction, guardrail bypass
- **Techniques**: Direct prompt injection, social engineering, encoding tricks
- **Business impact**: Customer data breach, reputational damage, compliance violation

### Malicious Insider

An authenticated user with legitimate but limited access who attempts to exceed their authorization.

- **Access level**: Standard user account, normal permissions
- **Primary goals**: Cross-user data access, privilege escalation, unauthorized actions
- **Techniques**: Authority claim escalation, context manipulation, tool abuse
- **Business impact**: Internal data breach, financial loss, lateral movement

### Compromised Account

A legitimate account that has been taken over by an external attacker. The attacker has the user's normal access and is attempting to escalate.

- **Access level**: Full authenticated access for that user role
- **Primary goals**: Maximum data extraction, persistent access, lateral movement
- **Techniques**: All insider techniques plus credential harvesting, session manipulation
- **Business impact**: Full-scope data breach, persistent compromise, supply chain attack

### Disgruntled Employee

An insider with deep system knowledge who is motivated by grievance rather than financial gain.

- **Access level**: May have elevated privileges, deep knowledge of internal systems
- **Primary goals**: Sabotage, data destruction, reputational damage
- **Techniques**: Knowledge base poisoning, output manipulation, process disruption
- **Business impact**: Data integrity compromise, operational disruption, reputational damage

### Supply Chain Attacker

An attacker who targets the AI system indirectly through a connected service, data source, or integration.

- **Access level**: No direct access; operates through a compromised upstream source
- **Primary goals**: Indirect injection, data poisoning, persistent backdoor
- **Techniques**: RAG poisoning, tool output manipulation, MCP compromise
- **Business impact**: Persistent compromise, supply chain contamination, undetected exfiltration

## How Personas Drive Testing

During test generation (Stage 6), the selected persona influences:

1. **Payload framing** — The authority claims, terminology, and scenario context used
2. **Evasion strategy selection** — Which bypass techniques are realistic for this persona
3. **Outcome targeting** — Which business outcomes this persona would pursue
4. **Chain construction** — Which attack chain templates apply to this access level

The result is test plans that reflect realistic threat scenarios rather than theoretical vulnerability catalogs.
