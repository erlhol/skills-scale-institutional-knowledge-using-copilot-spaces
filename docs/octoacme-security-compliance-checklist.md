# OctoACME Security & Compliance Checklist

**Document Purpose:** Integrate security and compliance gates throughout the project lifecycle, aligned with OWASP Top 10 (2025 Edition) and industry best practices.

**Owner:** Security Champion  
**Stakeholders:** Project Manager, QA Lead, Development Lead, Compliance Officer  
**Last Updated:** 2026-05-02

---

## Table of Contents
1. [Security Governance](#security-governance)
2. [OWASP Top 10 (2025) Mapping](#owasp-top-10-2025-mapping)
3. [Security Gates by Project Phase](#security-gates-by-project-phase)
4. [Threat Assessment Framework](#threat-assessment-framework)
5. [Risk Rating & Escalation](#risk-rating--escalation)
6. [Compliance Checkpoints](#compliance-checkpoints)
7. [Security Champion Responsibilities](#security-champion-responsibilities)

---

## Security Governance

### Core Principles
- **Security by Design:** Security is embedded from project initiation, not added later
- **Defense in Depth:** Multiple layers of security controls at each phase
- **Least Privilege:** Access and permissions follow minimum-necessary principle
- **Zero Trust:** Assume no implicit trust; verify all interactions
- **Transparency:** All security decisions are documented and traceable

### RACI for Security Decisions
| Role | Responsibility |
|------|-----------------|
| **Security Champion** | Responsible & Accountable for security strategy and approvals |
| **Project Manager** | Accountable for schedule impact; Responsible for security planning |
| **QA Lead** | Responsible for security testing and validation |
| **Development Lead** | Responsible for implementing security controls |
| **Compliance Officer** | Consulted on regulatory requirements; Informed of risks |

---

## OWASP Top 10 (2025) Mapping

The following OWASP Top 10 2025 vulnerabilities are addressed at specific project phases:

### **A01: Broken Access Control**
- **Definition:** Users can act outside intended permissions
- **Detection Phase:** Project Planning & Execution
- **Control:** Role-based access control (RBAC) matrix; principle of least privilege
- **Gate:** Access control design review before development
- **Testing:** Unauthorized access attempt testing in QA

### **A02: Cryptographic Failures**
- **Definition:** Sensitive data exposed due to weak/missing encryption
- **Detection Phase:** Project Initiation & Planning
- **Control:** Data classification; encryption standards (AES-256, TLS 1.3+)
- **Gate:** Data flow diagram review; encryption requirement sign-off
- **Testing:** Cryptographic validation in security testing

### **A03: Injection**
- **Definition:** Untrusted data interpreted as executable code (SQL, NoSQL, command injection)
- **Detection Phase:** Project Planning & Execution
- **Control:** Input validation; parameterized queries; no dynamic SQL
- **Gate:** Code review focus on injection vectors
- **Testing:** OWASP Top 10 injection test cases in QA phase

### **A04: Insecure Design**
- **Definition:** Missing or ineffective security controls in design phase
- **Detection Phase:** Project Initiation (Threat Modeling)
- **Control:** Threat modeling (STRIDE methodology); security architecture review
- **Gate:** Threat model approved before development begins
- **Testing:** Design security controls verified in execution phase

### **A05: Security Misconfiguration**
- **Definition:** Insecure default configurations, unnecessary features, or unpatched systems
- **Detection Phase:** Project Planning & Release
- **Control:** Security configuration baselines; hardening guides; automated scanning
- **Gate:** Infrastructure security review before deployment
- **Testing:** Configuration scanning and vulnerability assessment

### **A06: Vulnerable & Outdated Components**
- **Definition:** Known vulnerabilities in dependencies and third-party libraries
- **Detection Phase:** Project Planning & Execution
- **Control:** Dependency inventory; software composition analysis (SCA)
- **Gate:** Approved vendor/library list; quarterly dependency audit
- **Testing:** Automated SCA in CI/CD pipeline; SBOM generation

### **A07: Authentication & Session Management Failures**
- **Definition:** Session hijacking, weak credentials, insecure token handling
- **Detection Phase:** Project Planning & Execution
- **Control:** Multi-factor authentication (MFA); secure session management; OAuth 2.0/OIDC
- **Gate:** Authentication architecture review
- **Testing:** Session hijacking, brute force, credential stuffing tests

### **A08: Software & Data Integrity Failures**
- **Definition:** Insecure CI/CD pipelines, unsigned updates, compromised dependencies
- **Detection Phase:** Project Planning & Release
- **Control:** Code signing; binary verification; secure artifact storage
- **Gate:** CI/CD security hardening review
- **Testing:** Supply chain integrity validation

### **A09: Logging & Monitoring Failures**
- **Definition:** Insufficient logging, monitoring, and alerting for security events
- **Detection Phase:** Project Planning & Execution
- **Control:** Centralized logging; security event monitoring (SIEM); incident response plan
- **Gate:** Logging & monitoring architecture review
- **Testing:** Log completeness and integrity validation

### **A10: Server-Side Request Forgery (SSRF)**
- **Definition:** Application fetches remote resources without validating URLs
- **Detection Phase:** Project Planning & Execution
- **Control:** URL validation; network segmentation; allowlist enforcement
- **Gate:** SSRF risk assessment in threat modeling
- **Testing:** SSRF attack simulation in security testing

---

## Security Gates by Project Phase

### **Phase 1: Initiation**
#### Security Checkpoint: Project Intake & Risk Assessment

**Activities:**
- [ ] Identify data classification levels (Public, Internal, Confidential, Restricted)
- [ ] Initial risk assessment: Does this project handle sensitive data or critical systems?
- [ ] Determine regulatory requirements (GDPR, HIPAA, PCI-DSS, SOC 2, etc.)
- [ ] Identify external dependencies and third-party integrations
- [ ] Assign Security Champion if not already assigned
- [ ] Document security assumptions and constraints

**Responsible:** Security Champion, Project Manager  
**Approval Required:** Yes (Security Champion sign-off)

**Template:** [Security Initiation Checklist](#appendix-a-security-initiation-checklist)

---

### **Phase 2: Planning**
#### Security Checkpoint: Threat Modeling & Architecture Review

**Activities:**
- [ ] Conduct threat modeling using STRIDE methodology (see `octoacme-threat-modeling-requirements.md`)
- [ ] Document data flows and trust boundaries
- [ ] Create/update security architecture diagram
- [ ] Define authentication and authorization mechanisms
- [ ] Identify encryption requirements (data at rest, in transit)
- [ ] Define logging and monitoring strategy
- [ ] Create RACI matrix for security responsibilities
- [ ] Establish security acceptance criteria (SAC) for each user story
- [ ] Dependency audit: Identify approved vs. risky components

**Responsible:** Security Champion, Development Lead, QA Lead  
**Approval Required:** Yes (Threat model approved)

**Deliverables:**
- Threat Model Report (STRIDE)
- Security Architecture Diagram
- Data Classification Matrix
- Approved Dependency List

---

### **Phase 3: Execution & Development**
#### Security Checkpoint: Secure Coding & Code Review

**Activities:**
- [ ] Implement security controls per threat model
- [ ] Follow secure coding guidelines (OWASP Secure Coding Practices)
- [ ] Enforce input validation and output encoding
- [ ] Use parameterized queries (prevent SQL injection)
- [ ] Implement proper access controls (RBAC)
- [ ] Enable security logging for all sensitive operations
- [ ] Conduct peer code reviews with security focus
- [ ] Run static application security testing (SAST) tools
- [ ] Track and remediate SAST findings
- [ ] Document security decisions and exceptions

**Responsible:** Development Lead, QA Lead  
**Approval Required:** Code review approval from peer + Security Champion spot-checks

**Tools:**
- SAST: SonarQube, Semgrep, GitHub Code Scanning
- Dependency Scanning: Dependabot, Snyk
- Secret Detection: GitGuardian, TruffleHog

---

### **Phase 4: Testing & QA**
#### Security Checkpoint: Security Testing & Validation

**Activities:**
- [ ] Execute security test cases (OWASP Top 10)
- [ ] Conduct dynamic application security testing (DAST)
- [ ] Perform penetration testing on critical components
- [ ] Validate encryption implementation
- [ ] Test authentication and session management flows
- [ ] Verify logging and monitoring functionality
- [ ] Validate error handling (no sensitive data leakage)
- [ ] Test access control boundaries
- [ ] Perform configuration security review
- [ ] Execute supply chain security validation (SBOM verification)

**Responsible:** QA Lead, Security Champion  
**Approval Required:** Yes (Security testing sign-off)

**Test Coverage:**
- [ ] OWASP Top 10 (2025) test cases
- [ ] Injection testing (SQL, NoSQL, Command)
- [ ] Authentication brute force, session hijacking
- [ ] Authorization bypass attempts
- [ ] Cryptographic validation
- [ ] Sensitive data exposure scenarios

---

### **Phase 5: Release & Deployment**
#### Security Checkpoint: Release Security Review

**Activities:**
- [ ] Final security sign-off review
- [ ] Validate all security findings are resolved or documented
- [ ] Review deployment security checklist
- [ ] Verify infrastructure hardening (OS patches, firewall rules, secrets management)
- [ ] Validate rollback plan includes security rollback procedures
- [ ] Enable monitoring and alerting in production
- [ ] Document deployment security decisions
- [ ] Conduct post-deployment security validation
- [ ] Verify incident response procedures are in place

**Responsible:** Security Champion, Operations/DevOps  
**Approval Required:** Yes (Release security sign-off)

**Pre-Deployment Validation:**
- [ ] Infrastructure vulnerability scan completed
- [ ] Configuration hardening verified
- [ ] Secrets stored in secure vault (never in code)
- [ ] SSL/TLS certificates valid and modern (TLS 1.2+)
- [ ] WAF/IDS rules configured and tested
- [ ] Monitoring and alerting active

---

### **Phase 6: Retrospective & Continuous Improvement**
#### Security Checkpoint: Security Lessons Learned

**Activities:**
- [ ] Review security findings and root causes
- [ ] Document security incidents (if any) and response time
- [ ] Assess effectiveness of security controls
- [ ] Identify process improvements for next iteration
- [ ] Update threat model if design changed
- [ ] Evaluate new OWASP guidance or threat landscape changes
- [ ] Plan security enhancements for next phase
- [ ] Share learnings with broader team

**Responsible:** Security Champion, Project Manager  
**Approval Required:** Process review and documentation

---

## Threat Assessment Framework

### Risk Rating Matrix

**Severity Levels:**
- **CRITICAL:** Immediate threat to data, system integrity, or compliance; requires emergency remediation
- **HIGH:** Significant vulnerability that could lead to data breach or system compromise; must remediate before release
- **MEDIUM:** Moderate risk; should be addressed in current or next iteration
- **LOW:** Minor vulnerability; can be tracked and addressed in future sprints
- **INFORMATIONAL:** Observation or best practice recommendation

### CVSS v4.0 Integration

For all identified vulnerabilities, use CVSS v4.0 scoring:
- **CVSS Score 9.0-10.0:** CRITICAL
- **CVSS Score 7.0-8.9:** HIGH
- **CVSS Score 4.0-6.9:** MEDIUM
- **CVSS Score 0.1-3.9:** LOW

---

## Risk Rating & Escalation

### Escalation Triggers

| Trigger | Action | Owner |
|---------|--------|-------|
| CRITICAL finding | Immediate escalation to CTO/Security Lead | Security Champion |
| Finding affects data classification Restricted | Escalate to Compliance Officer | Security Champion |
| Finding violates regulatory requirement | Escalate to Legal/Compliance | Security Champion |
| Finding requires architecture change | Escalate to Project Manager + CTO | Security Champion |
| Finding discovered in production | Execute Incident Response Plan | Security Champion |

### Escalation Contacts
- **Security Champion:** [Contact Info]
- **CTO/Security Lead:** [Contact Info]
- **Compliance Officer:** [Contact Info]
- **Incident Response Lead:** [Contact Info]

---

## Compliance Checkpoints

### Regulatory Frameworks

**Check the following for your project:**

- [ ] **GDPR (EU):** Personal data handling, right to deletion, privacy by design
- [ ] **CCPA/CPRA (California):** Consumer privacy rights, data disclosure
- [ ] **HIPAA (US Healthcare):** Protected health information (PHI) handling
- [ ] **PCI-DSS (Payment Cards):** Cardholder data protection if processing payments
- [ ] **SOC 2:** Security, availability, processing integrity (if serving enterprise clients)
- [ ] **NIST Cybersecurity Framework:** Risk management alignment
- [ ] **ISO 27001:** Information security management system
- [ ] **Industry-Specific Standards:** (FinTech, Healthcare, Government, etc.)

### Compliance Validation

**Before Release:**
- [ ] Privacy Impact Assessment (PIA) completed
- [ ] Data residency requirements documented
- [ ] Data retention policies enforced
- [ ] Audit logging configured for compliance audit trails
- [ ] Third-party vendor compliance verified
- [ ] Incident response plan documented and tested

---

## Security Champion Responsibilities

### Core Accountabilities
1. **Security Strategy:** Define and communicate security vision for the project
2. **Gate Approvals:** Approve threat models, security architecture, testing, and release decisions
3. **Escalation:** Identify and escalate security risks and findings
4. **Education:** Coach team on secure coding, OWASP principles, and threat awareness
5. **Incident Response:** Lead response to security events
6. **Continuous Improvement:** Monitor emerging threats and update security practices

### Key Interactions
- **With Project Manager:** Align security requirements with schedule and scope
- **With Development Lead:** Review security architecture and code security practices
- **With QA Lead:** Define security test cases and validate findings
- **With Compliance Officer:** Ensure regulatory requirements are met
- **With Operations/DevOps:** Harden infrastructure and enable monitoring

### Monthly Responsibilities
- [ ] Review and triage security findings
- [ ] Update threat landscape assessment
- [ ] Conduct security knowledge-sharing session
- [ ] Audit compliance with security gate processes
- [ ] Report security metrics to leadership

---

## Appendix A: Security Initiation Checklist

```
PROJECT: ________________________________     DATE: ____________________

1. DATA CLASSIFICATION & SENSITIVITY
   [ ] Public data only
   [ ] Internal data (not sensitive)
   [ ] Confidential data (customer or proprietary)
   [ ] Restricted data (highly sensitive - PII, PHI, financial)

2. REGULATORY REQUIREMENTS
   [ ] None identified
   [ ] GDPR (EU personal data)
   [ ] CCPA/CPRA (California resident data)
   [ ] HIPAA (Healthcare)
   [ ] PCI-DSS (Payment cards)
   [ ] SOC 2 (If serving enterprises)
   [ ] Other: ________________________________

3. EXTERNAL DEPENDENCIES & INTEGRATIONS
   List third-party services, APIs, vendors:
   ________________________________
   ________________________________

4. SECURITY CHAMPION ASSIGNMENT
   Name: ________________________________     Contact: ____________________

5. INITIAL RISK ASSESSMENT
   Key Risks Identified:
   ________________________________
   ________________________________

Approved By: ________________________________     Date: ____________________
```

---

## Appendix B: Security Approval Sign-Off Template

```
PROJECT: ________________________     PHASE: ____________________
SECURITY GATE: ________________________     DATE: ____________________

GATE REQUIREMENTS:
[ ] All items completed
[ ] No open CRITICAL findings
[ ] All HIGH findings have remediation plan with timeline
[ ] Threat model (if applicable) approved
[ ] Security testing complete
[ ] Compliance checkpoints validated

FINDINGS SUMMARY:
- CRITICAL: ____  (count)
- HIGH: ____  (count)
- MEDIUM: ____  (count)
- LOW: ____  (count)

SIGN-OFF:
Security Champion: ________________________________     Date: ____________________

ESCALATIONS (if any):
[ ] CTO/Security Lead notified
[ ] Compliance Officer notified
[ ] Project Manager notified

Comments/Notes:
_________________________________________________________________
_________________________________________________________________

APPROVAL: [ ] APPROVED   [ ] APPROVED WITH CONDITIONS   [ ] HOLD FOR REMEDIATION
```

---

## References
- [OWASP Top 10 (2025)](https://owasp.org/www-project-top-ten/)
- [OWASP Secure Coding Practices](https://owasp.org/www-project-secure-coding-practices/)
- [OWASP Threat Modeling](https://owasp.org/www-community/Threat_Modeling)
- [CVSS v4.0 Calculator](https://www.first.org/cvss/v4.0/calculator)
- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)