# OctoACME Threat Modeling Requirements

**Document Purpose:** Establish mandatory threat modeling processes using OWASP methodologies to identify, analyze, and mitigate security threats across all project phases.

**Owner:** Security Champion  
**Stakeholders:** Development Lead, Project Manager, QA Lead, Architecture Lead  
**Last Updated:** 2026-05-02

---

## Table of Contents
1. [Threat Modeling Governance](#threat-modeling-governance)
2. [Threat Modeling Methodology (STRIDE)](#threat-modeling-methodology-stride)
3. [Threat Modeling by Project Phase](#threat-modeling-by-project-phase)
4. [Creating Data Flow Diagrams (DFDs)](#creating-data-flow-diagrams-dfds)
5. [Threat Identification & Analysis](#threat-identification--analysis)
6. [Risk Rating & Prioritization](#risk-rating--prioritization)
7. [Mitigation Strategies](#mitigation-strategies)
8. [Threat Modeling Artifacts](#threat-modeling-artifacts)

---

## Threat Modeling Governance

### Threat Modeling Principles
- **Proactive:** Identify threats early in design phase, not during implementation
- **Comprehensive:** Consider all assets, threat actors, and attack vectors
- **Structured:** Use STRIDE methodology for systematic analysis
- **Documented:** All threats and mitigations are recorded
- **Collaborative:** Involve cross-functional team (dev, security, architecture)
- **Iterative:** Update threat model as design evolves
- **Actionable:** Every threat has documented mitigation or acceptance

### Who Participates in Threat Modeling?
- **Security Champion** (facilitator, overall owner)
- **Development Lead** (architecture, implementation perspective)
- **Project Manager** (timeline, feasibility)
- **QA Lead** (testing perspective, attack vectors)
- **Architect/Tech Lead** (system design)
- **Product Owner** (business context)

### When to Conduct Threat Modeling?

**MANDATORY:**
- [ ] Every new feature with data handling
- [ ] Every new external integration
- [ ] Every API or service creation
- [ ] Every architecture change
- [ ] Every new third-party library integration

**OPTIONAL:**
- [ ] UI/UX improvements (unless data handling involved)
- [ ] Performance optimizations (unless architecture changed)
- [ ] Bug fixes (unless security-critical)

---

## Threat Modeling Methodology (STRIDE)

### STRIDE Framework Overview

STRIDE is a systematic approach to identify threats across six categories:

| Category | Definition | Example |
|----------|-----------|---------|
| **Spoofing** | Attacker pretends to be someone/something they're not | Fake authentication credentials |
| **Tampering** | Attacker modifies data or code | Modifying request parameters, MitM attacks |
| **Repudiation** | Attacker denies performing an action | User denies making transaction |
| **Information Disclosure** | Sensitive data exposed to unauthorized parties | SQL injection revealing customer data |
| **Denial of Service** | Attacker prevents legitimate access | DDoS, resource exhaustion |
| **Elevation of Privilege** | Attacker gains higher permissions than intended | User escalates to admin |

### STRIDE Analysis Process

```
1. DECOMPOSE SYSTEM
   ├─ Create/update Data Flow Diagram (DFD)
   ├─ Identify trust boundaries
   ├─ Map data stores and flows
   └─ Identify entry/exit points

2. IDENTIFY THREATS
   ├─ Apply STRIDE to each component
   ├─ Consider threat actors
   ├─ Document attack vectors
   └─ List potential threats

3. ANALYZE THREATS
   ├─ Assess likelihood
   ├─ Assess impact
   ├─ Calculate risk score (CVSS v4.0)
   └─ Prioritize threats

4. CREATE MITIGATIONS
   ├─ For each threat, define control(s)
   ├─ Assign responsibility
   ├─ Set implementation timeline
   └─ Define acceptance criteria

5. DOCUMENT & REVIEW
   ├─ Create threat model document
   ├─ Obtain approval from stakeholders
   ├─ Communicate findings to team
   └─ Monitor mitigation implementation
```

---

## Threat Modeling by Project Phase

### Phase 1: Initiation - Preliminary Threat Assessment

**When:** During project kickoff  
**Participants:** Security Champion, Project Manager, Product Owner  
**Deliverable:** Preliminary Threat Assessment

**Scope:**
- Identify high-level data classifications
- Preliminary external dependencies
- Known compliance requirements
- Initial threat landscape

**Output:**
```
PROJECT: [Name]
DATA CLASSIFICATION: [ ] Public  [ ] Internal  [ ] Confidential  [ ] Restricted
EXTERNAL INTEGRATIONS: [List any known third-party services]
REGULATORY SCOPE: [ ] GDPR  [ ] HIPAA  [ ] PCI-DSS  [ ] SOC 2  [ ] Other: _____

PRELIMINARY THREATS (High-level):
1. [Threat area 1]
2. [Threat area 2]
3. [Threat area 3]

NEXT STEPS: → Proceed to Planning phase for comprehensive threat modeling
```

---

### Phase 2: Planning - Comprehensive Threat Modeling

**When:** During sprint planning, before development starts  
**Participants:** Security Champion, Development Lead, Architect, QA Lead  
**Duration:** 4-8 hours for typical features  
**Deliverable:** Threat Model Report with DFD, STRIDE analysis, and mitigations

#### Step 1: Create Data Flow Diagram (DFD)

Create a DFD showing:
- [ ] External entities (users, systems, services)
- [ ] Processes (components handling data)
- [ ] Data stores (databases, caches)
- [ ] Data flows (movement between components)
- [ ] Trust boundaries (security perimeter)

**DFD Example:**
```
[User] →(HTTP/S)→ [Web App] →(SQL)→ [Database]
                       ↓
                  [Auth Service]
                       ↑
                  [API Gateway]
```

**Trust Boundaries:**
```
┌──────────────────���──────────────────────┐
│   TRUSTED INTERNAL NETWORK              │
│                                         │
│  [Web App] ←→ [Auth Service]           │
│       ↓                ↓                │
│  [Database]    [Cache Layer]           │
└─────────────────────────────────────────┘
              ↑ (Internet boundary)
[Untrusted User/External API]
```

#### Step 2: Apply STRIDE to Each Component

**Template:**
```
COMPONENT: [Component Name]
TRUST BOUNDARY: [ ] Inside  [ ] Crosses boundary

STRIDE THREATS:

S - SPOOFING
  [ ] Threat: [Describe threat]
      → Example: Attacker impersonates legitimate user
      → Attack vector: Weak password, stolen credentials
      → Impact: Unauthorized access to user data

T - TAMPERING
  [ ] Threat: [Describe threat]
      → Example: Attacker modifies data in transit
      → Attack vector: Man-in-the-Middle (MitM) attack
      → Impact: Data integrity violation

R - REPUDIATION
  [ ] Threat: [Describe threat]
      → Example: User claims they didn't perform action
      → Attack vector: Missing audit logging
      → Impact: Accountability loss, compliance violation

I - INFORMATION DISCLOSURE
  [ ] Threat: [Describe threat]
      → Example: Sensitive data exposed in error messages
      → Attack vector: Exception stack traces
      → Impact: Information leakage (PII, credentials)

D - DENIAL OF SERVICE
  [ ] Threat: [Describe threat]
      → Example: Attacker floods API with requests
      → Attack vector: No rate limiting
      → Impact: Service unavailability

E - ELEVATION OF PRIVILEGE
  [ ] Threat: [Describe threat]
      → Example: Regular user escalates to admin
      → Attack vector: Broken access control
      → Impact: Unauthorized system access
```

#### Step 3: Rate Threats Using CVSS v4.0

For each threat identified, calculate CVSS v4.0 score:

**CVSS Scoring Factors:**
- Attack Vector (AV): Network, Adjacent, Local, Physical
- Attack Complexity (AC): Low or High
- Privileges Required (PR): None, Low, High
- User Interaction (UI): None or Required
- Scope (S): Unchanged or Changed
- Confidentiality Impact (C): None, Low, High
- Integrity Impact (I): None, Low, High
- Availability Impact (A): None, Low, High

**CVSS Score Mapping to Severity:**
- 9.0-10.0: CRITICAL
- 7.0-8.9: HIGH
- 4.0-6.9: MEDIUM
- 0.1-3.9: LOW
- 0.0: NONE

**Use [CVSS v4.0 Calculator](https://www.first.org/cvss/v4.0/calculator) to calculate scores.**

---

### Phase 3: Execution - Threat Model Updates

**When:** During development, if design changes  
**Participants:** Security Champion, Development Lead  
**Frequency:** As-needed when architecture changes

**Update Trigger:** If any of these change:
- [ ] Architecture modified
- [ ] New external integration added
- [ ] Data classification changed
- [ ] Authentication/authorization redesigned
- [ ] Infrastructure changed

**Update Process:**
1. Identify changed components
2. Re-apply STRIDE analysis to changes
3. Assess new/updated threats
4. Update mitigations if needed
5. Obtain approval for significant changes

---

### Phase 4: Testing - Threat-Based Test Case Generation

**When:** During QA phase  
**Participants:** QA Lead, Security Champion  
**Deliverable:** Security test cases based on threat model

**Process:**
1. For each identified THREAT, create test case
2. For each MITIGATION, create validation test case
3. Execute test cases during security testing phase

**Example Test Cases from Threat Model:**

```
THREAT: SQL Injection in login form
MITIGATION: Use parameterized queries
TEST CASE:
  Input: admin' OR '1'='1
  Expected: Input treated as literal string, not SQL code
  Result: [ ] PASS  [ ] FAIL

THREAT: Session hijacking via unencrypted cookies
MITIGATION: Use HttpOnly, Secure flags on cookies
TEST CASE:
  Verify: Cookie has HttpOnly flag set
  Verify: Cookie has Secure flag set (HTTPS only)
  Result: [ ] PASS  [ ] FAIL
```

---

### Phase 5: Release - Pre-Deployment Threat Review

**When:** Before production deployment  
**Participants:** Security Champion, Development Lead, Operations  
**Checklist:**

- [ ] All CRITICAL threats have mitigations implemented
- [ ] All HIGH threats have mitigations or documented acceptance
- [ ] Threat model reflects final implementation
- [ ] Security architecture validated in staging
- [ ] Monitoring configured to detect threat exploitation
- [ ] Incident response plan considers key threats
- [ ] No unacceptable risk remains

---

## Creating Data Flow Diagrams (DFDs)

### DFD Components

**External Entity:** Outside system or user
```
   ┌─────────┐
   │  User   │
   │ (Actor) │
   └─────────┘
```

**Process:** Component handling/transforming data
```
   ┌──────────────┐
   │   Process    │
   │ (e.g., Auth) │
   └──────────────┘
```

**Data Store:** Where data persists
```
   ┌────────────────────┐
   │ ══════════════════ │
   │  Database / Cache  │
   │ ══════════════════ │
   └────────────────────┘
```

**Data Flow:** Movement of data
```
   Source ────data flow──→ Destination
              (labeled)
```

### DFD Example: User Authentication Flow

```
                                 ┌─────────────────┐
                                 │  Database       │
                                 │ [Credentials]   │
                                 └────────┬────────┘
                                          │
                                   (SQL queries)
                                          │
   ┌──────────┐    (HTTP/S)    ┌─────────▼────────┐
   │  User    │◄───login───────│  Web App         │
   │ (Actor)  │                │ [Auth Service]   │
   └──────────┘    response    └────────┬─────────┘
                                        │
                                   (decrypted)
                                        │
                                 ┌──────▼────────┐
                                 │  Cache Layer  │
                                 │  [Session]    │
                                 └───────────────┘

TRUST BOUNDARIES:
  Internet boundary: Between User and Web App
  Internal boundary: Between Web App and Database/Cache
```

### DFD Best Practices

✅ **DO:**
- Show all external entities
- Include all data flows clearly
- Label data flows with data type/sensitivity
- Mark trust boundaries explicitly
- Keep DFD simple and readable
- Create separate DFDs for different use cases
- Update DFD as architecture evolves

❌ **DON'T:**
- Include implementation details
- Make DFD overly complex
- Forget data stores or processes
- Omit trust boundaries
- Leave data flows unlabeled

---

## Threat Identification & Analysis

### Threat Identification Checklist

For each component and data flow, ask:

**Spoofing:**
- [ ] Can attacker impersonate a legitimate user?
- [ ] Are credentials stored securely?
- [ ] Is authentication enforced at all entry points?
- [ ] Can attacker create fake accounts?

**Tampering:**
- [ ] Can attacker modify data in transit?
- [ ] Is data encrypted (TLS/HTTPS)?
- [ ] Is data integrity verified (HMAC/signature)?
- [ ] Can attacker modify data at rest?

**Repudiation:**
- [ ] Is user action logged?
- [ ] Can logs be tampered with?
- [ ] Is timestamping in place?
- [ ] Can user deny performing an action?

**Information Disclosure:**
- [ ] Can sensitive data be exposed in transit?
- [ ] Can sensitive data be exposed at rest?
- [ ] Are error messages revealing system details?
- [ ] Can attacker access logs or backups?

**Denial of Service:**
- [ ] Can attacker overwhelm the service?
- [ ] Are rate limits enforced?
- [ ] Is resource consumption bounded?
- [ ] Are there retry limits?

**Elevation of Privilege:**
- [ ] Can attacker gain unauthorized permissions?
- [ ] Are permission checks enforced?
- [ ] Is least privilege implemented?
- [ ] Can attacker exploit misconfigurations?

---

## Risk Rating & Prioritization

### Risk Matrix: Likelihood × Impact

```
                     LIKELIHOOD
           Low    Medium    High
       ┌─────────────────────────┐
   H   │  M      H       C       │  Confidentiality
   I I │  M      H       C       │  Integrity
   G H │  L      M       H       │  Availability
   H I │  L      M       H       │  Reputation
       └─────────────────────────┘

Legend:
  C = CRITICAL (address immediately)
  H = HIGH (address before release)
  M = MEDIUM (address in current/next sprint)
  L = LOW (track and address in future)
```

### Prioritization Criteria

**Address IMMEDIATELY (CRITICAL):**
- Authentication bypass vulnerabilities
- SQL injection or code injection flaws
- Data exposure of Restricted data
- Zero-day exploits

**Address BEFORE RELEASE (HIGH):**
- Broken access control
- Weak cryptography
- Missing logging of security events
- Unpatched dependencies with known exploits

**Address SOON (MEDIUM):**
- Sensitive data in error messages
- Weak password policies
- CORS misconfigurations
- Rate limiting not implemented

**Address OPPORTUNISTICALLY (LOW):**
- Missing security headers
- Suggestion for defense-in-depth
- Best practice recommendations

---

## Mitigation Strategies

### Mitigation Template

```
THREAT ID: T-001
THREAT: [Description]
SEVERITY: [ ] CRITICAL  [ ] HIGH  [ ] MEDIUM  [ ] LOW
CVSS SCORE: 7.5

MITIGATIONS (choose one or more):

1. PREVENTIVE CONTROL (prevent threat from occurring)
   Control: [Describe control]
   Example: Use parameterized SQL queries
   Owner: Development Lead
   Acceptance Criteria:
   - [ ] All database queries use parameterized statements
   - [ ] Code review confirms no dynamic SQL
   - [ ] Automated SAST scanning passes
   Timeline: This sprint

2. DETECTIVE CONTROL (identify threat if it occurs)
   Control: [Describe control]
   Example: Enable SQL injection detection in WAF
   Owner: Operations/Security
   Acceptance Criteria:
   - [ ] WAF rules configured
   - [ ] Alerts firing for injection attempts
   - [ ] Log review shows detection working
   Timeline: Before production deployment

3. CORRECTIVE CONTROL (remediate after threat occurs)
   Control: [Describe control]
   Example: Incident response plan for SQL injection
   Owner: Security Champion
   Acceptance Criteria:
   - [ ] Incident playbook created
   - [ ] Team trained on response
   - [ ] Communication templates prepared
   Timeline: Before production deployment

4. RISK ACCEPTANCE (accept residual risk)
   Rationale: [Why accepting this risk]
   Approval: [Who approved acceptance]
   Conditions: [Any conditions on acceptance]
   Review Date: [When to re-assess]
   Timeline: [If applicable]

SELECTED MITIGATION: [Choose option 1, 2, 3, or 4]
OWNER: [Name]
DUE DATE: [Date]
STATUS: [ ] Not Started  [ ] In Progress  [ ] Complete  [ ] Accepted Risk
```

### Mitigation Categories (OWASP-aligned)

| Category | Techniques |
|----------|-----------|
| **Input Validation** | Whitelist validation, length checks, format validation, encoding |
| **Output Encoding** | HTML encoding, URL encoding, JavaScript encoding |
| **Authentication** | MFA, strong password policy, secure session management, OAuth 2.0/OIDC |
| **Authorization** | Role-Based Access Control (RBAC), principle of least privilege, ABAC |
| **Encryption** | AES-256 at rest, TLS 1.2+ in transit, strong key management |
| **Logging & Monitoring** | Centralized logging, SIEM, alerting, audit trails |
| **Dependency Management** | SCA scanning, approved components list, regular updates |
| **Secure Development** | Code review, SAST/DAST, secure coding guidelines, threat modeling |

---

## Threat Modeling Artifacts

### Artifact 1: Threat Model Report

**Contents:**
- Executive summary
- DFD (Data Flow Diagram)
- STRIDE analysis by component
- Threat list with CVSS scores
- Mitigations and owners
- Risk matrix
- Approval sign-offs

### Artifact 2: Risk Register

**Template:**
```
RISK ID | THREAT | SEVERITY | OWNER | MITIGATION | STATUS | TARGET DATE
TR-001  | [...]  | HIGH     | [...]| [...]      | [...] | [...]
TR-002  | [...]  | MEDIUM   | [...]| [...]      | [...] | [...]
```

### Artifact 3: Threat Model Approval Sign-Off

```
PROJECT: _________________________     DATE: ____________________
THREAT MODEL VERSION: 1.0

THREAT MODEL REVIEW COMPLETED:
[ ] DFD created and validated
[ ] STRIDE analysis complete
[ ] All threats rated (CVSS)
[ ] Mitigations defined
[ ] Owners assigned
[ ] Timeline planned

APPROVALS:
Security Champion: ________________________     Date: ____________________
Development Lead: ________________________     Date: ____________________
Project Manager: ________________________     Date: ____________________
(Add other stakeholders as needed)

APPROVED FOR: [ ] Development  [ ] Staging  [ ] Production

NEXT REVIEW DATE: ____________________

NOTES/CONDITIONS:
_________________________________________________________________
```

---

## References
- [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- [Microsoft STRIDE Methodology](https://learn.microsoft.com/en-us/azure/security/develop/threat-modeling-tool)
- [CVSS v4.0 Specification](https://www.first.org/cvss/v4.0/specification-document)
- [OWASP Top 10 (2025)](https://owasp.org/www-project-top-ten/)