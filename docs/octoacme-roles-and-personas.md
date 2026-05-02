# OctoACME Roles & Personas

**Document Purpose:** Define all key roles, responsibilities, accountabilities, and interactions within OctoACME project management framework. This document ensures clarity on who owns what, reducing ambiguity and enabling consistent project execution.

**Owner:** Project Manager / Stakeholder Engagement Owner  
**Last Updated:** 2026-05-02

---

## Table of Contents
1. [Core Roles Overview](#core-roles-overview)
2. [Traditional Project Management Roles](#traditional-project-management-roles)
3. [New Expanded Roles (Added May 2026)](#new-expanded-roles-added-may-2026)
4. [RACI Matrix by Process](#raci-matrix-by-process)
5. [Role Interactions & Communication](#role-interactions--communication)
6. [Accountability & Escalation](#accountability--escalation)

---

## Core Roles Overview

### Role Hierarchy

```
Executive Sponsor
        ↓
Project Manager ←─────────────────────────────┐
  │                                            │
  ├─→ Development Lead                        │
  ├─→ QA Lead                                 │
  ├─→ Security Champion (NEW)                 │
  ├─→ Change Control Coordinator (NEW)        │
  ├─→ Stakeholder Engagement Owner (NEW)      │
  └─→ Product Owner                           │
        ↓
  Development Team / Operations Team
```

---

## Traditional Project Management Roles

### 1. Executive Sponsor

**Purpose:** Provide executive oversight, remove blockers, make business decisions  
**Authority Level:** High  
**Reports To:** C-Suite

**Responsibilities:**
- [ ] Approve project charter and scope
- [ ] Allocate budget and resources
- [ ] Escalate organizational/business risks
- [ ] Approve major changes or scope adjustments
- [ ] Communicate project status to leadership
- [ ] Remove organizational blockers

**Accountability:**
- Project success against business objectives
- ROI and business value realization
- Budget adherence
- Strategic alignment

**Key Interactions:**
- Monthly: Receive project status report
- As-needed: Approve budget changes, resolve organizational blockers
- Quarterly: Review business value realization

**Escalation Path:** C-Suite / Board

---

### 2. Project Manager

**Purpose:** Orchestrate project execution, manage timeline/scope/budget, coordinate team  
**Authority Level:** Medium  
**Reports To:** Executive Sponsor

**Responsibilities:**
- [ ] Develop and maintain project plan
- [ ] Manage schedule and critical path
- [ ] Track budget and financial metrics
- [ ] Identify and manage project risks
- [ ] Escalate issues and blockers
- [ ] Coordinate cross-functional team
- [ ] Track status and report to stakeholders
- [ ] Manage change requests (with Change Control Coordinator)
- [ ] Ensure communication and transparency

**Accountability:**
- Project delivery on time, on budget, on scope
- Risk management and issue resolution
- Team coordination and communication
- Stakeholder satisfaction

**Key Interactions:**
- Daily: Team sync, issue triage
- Weekly: Stakeholder status, risk review
- Bi-weekly: Formal status report to Executive Sponsor
- Monthly: Budget and financial review

**Escalation Path:** Executive Sponsor

---

### 3. Product Owner

**Purpose:** Define requirements, prioritize features, ensure business value  
**Authority Level:** Medium  
**Reports To:** Executive Sponsor (or Product Management hierarchy)

**Responsibilities:**
- [ ] Define product vision and roadmap
- [ ] Create and prioritize user stories
- [ ] Define acceptance criteria (with team input)
- [ ] Make feature trade-off decisions
- [ ] Represent customer/user voice
- [ ] Accept completed stories
- [ ] Manage product backlog

**Accountability:**
- Business value delivered
- Customer satisfaction
- Feature alignment with business objectives
- Clear requirements definition

**Key Interactions:**
- Sprint Planning: Present prioritized backlog
- Sprint Standup: (as-needed) Clarify requirements
- Sprint Review: Accept completed features
- Weekly: Backlog refinement with Development Lead

**Escalation Path:** Executive Sponsor

---

### 4. Development Lead

**Purpose:** Lead technical design, guide development team, ensure code quality  
**Authority Level:** Medium (technical)  
**Reports To:** Project Manager

**Responsibilities:**
- [ ] Lead technical architecture and design
- [ ] Review code quality and architecture decisions
- [ ] Mentor development team
- [ ] Estimate development effort
- [ ] Identify technical risks and dependencies
- [ ] Implement secure coding practices
- [ ] Plan technical implementation approach
- [ ] Coordinate with Security Champion on architecture

**Accountability:**
- Code quality and architectural integrity
- Technical feasibility and estimates
- Team technical capability development
- Security architecture implementation

**Key Interactions:**
- Daily: Team code reviews, technical guidance
- Weekly: Architecture review (if design changes)
- Sprint Planning: Effort estimation, technical approach
- Quarterly: Technical debt assessment

**Escalation Path:** Project Manager → CTO

---

### 5. QA Lead

**Purpose:** Define and execute quality assurance strategy, ensure acceptance criteria met  
**Authority Level:** Medium (quality gate)  
**Reports To:** Project Manager

**Responsibilities:**
- [ ] Define QA strategy and testing approach
- [ ] Create and execute test cases
- [ ] Manage defect lifecycle
- [ ] Coordinate security testing (with Security Champion)
- [ ] Provide quality metrics and visibility
- [ ] Define acceptance criteria (with team)
- [ ] Gate quality for releases
- [ ] Automate testing where possible

**Accountability:**
- Quality metrics and defect escape rate
- Test coverage and execution
- Acceptance criteria validation
- Release quality gate

**Key Interactions:**
- Sprint Planning: Clarify acceptance criteria, plan testing
- Daily: Defect triage, testing progress
- Pre-release: Quality gate sign-off
- Post-release: Quality metrics, lessons learned

**Escalation Path:** Project Manager

---

## New Expanded Roles (Added May 2026)

### 6. Security Champion (NEW)

**Purpose:** Embed security throughout project lifecycle, ensure OWASP compliance, manage security risks  
**Authority Level:** Medium (security gate)  
**Reports To:** Security Lead / CISO (dotted) + Project Manager (solid)

**Responsibilities:**
- [ ] Define security strategy for project
- [ ] Conduct threat modeling (STRIDE methodology)
- [ ] Review security architecture
- [ ] Define security acceptance criteria
- [ ] Coordinate security testing (OWASP Top 10)
- [ ] Gate security for releases
- [ ] Educate team on secure coding practices
- [ ] Manage CVSS scoring and risk assessment
- [ ] Lead incident response (if security issues arise)
- [ ] Ensure compliance with security/privacy regulations
- [ ] Interface with Compliance/Legal teams

**Accountability:**
- Security of the delivered application
- Compliance with OWASP principles and standards
- Security testing execution and sign-off
- Threat model accuracy and completeness
- No CRITICAL security vulnerabilities post-release

**Key Interactions:**

| Frequency | With | Activity |
|-----------|------|----------|
| **Project Initiation** | PM, Dev Lead, Product Owner | Initial security assessment |
| **Sprint Planning** | Dev Lead, QA Lead | Security requirements for user stories |
| **Development Phase** | Dev Lead | Code review (security focus), secure coding guidance |
| **Testing Phase** | QA Lead | Security test case design, result analysis |
| **Pre-Release** | All leads | Final security gate review, approval |
| **Post-Release** | Ops, Incident Response | Monitoring, incident triage |

**Escalation Path:**
- Security findings: Project Manager, CISO
- CRITICAL vulnerabilities: CTO, CISO, Executive Sponsor

**Security Champion Activities by Phase:**

**Phase 1: Initiation**
- [ ] Data classification assessment
- [ ] Regulatory/compliance requirement identification
- [ ] Preliminary threat landscape review
- [ ] Initial risk assessment

**Phase 2: Planning**
- [ ] Threat modeling (STRIDE) complete
- [ ] Security architecture design
- [ ] Approval from Security/Compliance

**Phase 3: Execution**
- [ ] Secure coding reviews
- [ ] SAST/dependency scanning monitoring
- [ ] Architecture validation
- [ ] Knowledge sharing sessions

**Phase 4: Testing**
- [ ] Security test case execution
- [ ] Penetration testing (if needed)
- [ ] Vulnerability remediation oversight
- [ ] Security acceptance criteria validation

**Phase 5: Release**
- [ ] Security gate sign-off
- [ ] Deployment security checklist
- [ ] Monitoring configuration validation

**Phase 6: Retrospective**
- [ ] Security lessons learned
- [ ] Threat model effectiveness review
- [ ] Process improvements

---

### 7. Quality Assurance Lead (Enhanced/Clarified)

**Purpose:** [See Section 5 above]  
**Enhancement:** Now explicitly responsible for security testing coordination with Security Champion

**New Responsibilities (added to traditional QA):**
- [ ] Coordinate security testing execution with Security Champion
- [ ] Execute OWASP Top 10 test cases
- [ ] Validate security acceptance criteria
- [ ] Manage security defect lifecycle
- [ ] Report on security testing metrics

**Key Interaction Update:**
- **With Security Champion:** Define security test cases, execute tests, validate findings

---

### 8. Change Control Coordinator (NEW)

**Purpose:** Manage formal change processes, maintain traceability, coordinate approvals, ensure communication  
**Authority Level:** Medium (process authority)  
**Reports To:** Project Manager

**Responsibilities:**
- [ ] Receive and log all change requests
- [ ] Assess impact of proposed changes
- [ ] Coordinate stakeholder approvals
- [ ] Maintain change log and audit trail
- [ ] Schedule and communicate changes
- [ ] Track implementation progress
- [ ] Manage rollback procedures
- [ ] Document change decisions and rationale
- [ ] Report on change metrics

**Accountability:**
- Change traceability and audit compliance
- Stakeholder communication and coordination
- Change approval workflows followed
- Implementation timeline adherence
- Rollback readiness

**Key Interactions:**

| Frequency | With | Activity |
|-----------|------|----------|
| **Continuous** | All team members | Receive change requests, triage |
| **Weekly** | PM, Dev Lead, Security Champion | Impact assessment, approvals |
| **Pre-Implementation** | All stakeholders | Change communication |
| **Implementation** | Operations, Dev Lead | Coordinate execution |
| **Post-Implementation** | All stakeholders | Completion notification, verification |

**Escalation Path:**
- Approval delays: Project Manager, Executive Sponsor
- Implementation issues: Project Manager, Development Lead
- Rollback decisions: Project Manager, CTO

**Change Control Coordinator Activities:**

**Change Intake:**
- [ ] Log all change requests
- [ ] Validate completeness
- [ ] Assign change ID and priority

**Impact Assessment:**
- [ ] Assess technical impact
- [ ] Assess business impact
- [ ] Assess operational impact
- [ ] Determine approval path

**Approval Coordination:**
- [ ] Route to appropriate approvers
- [ ] Track approval status
- [ ] Escalate delays

**Communication:**
- [ ] Pre-implementation notification
- [ ] At-implementation status updates
- [ ] Completion notification
- [ ] Post-implementation lessons learned

---

### 9. Stakeholder Engagement Owner (NEW)

**Purpose:** Ensure stakeholder interests are represented, feedback loops active, conflicts resolved  
**Authority Level:** Medium (stakeholder voice)  
**Reports To:** Project Manager / Executive Sponsor

**Responsibilities:**
- [ ] Identify and register all stakeholders
- [ ] Assess stakeholder interests and impact
- [ ] Develop stakeholder engagement plan
- [ ] Execute regular stakeholder communication
- [ ] Gather and consolidate stakeholder feedback
- [ ] Escalate stakeholder concerns
- [ ] Facilitate conflict resolution
- [ ] Ensure stakeholder satisfaction
- [ ] Communicate project/product changes
- [ ] Manage stakeholder expectations

**Accountability:**
- Stakeholder satisfaction and engagement
- Feedback loop effectiveness
- Communication completeness
- Conflict resolution and escalation
- Risk mitigation for stakeholder-related issues

**Key Interactions:**

| Frequency | With | Activity |
|-----------|------|----------|
| **Project Initiation** | All stakeholders | Stakeholder identification, needs assessment |
| **Sprint Start** | Stakeholders | Roadmap/plan communication |
| **Monthly/Quarterly** | Stakeholders | Progress updates, feedback gathering |
| **Major Changes** | Stakeholders | Change communication, impact explanation |
| **Project Close** | Stakeholders | Lessons learned, outcomes communication |

**Escalation Path:**
- Stakeholder conflicts: Project Manager, Executive Sponsor
- Feedback indicating scope issues: Project Manager, Product Owner
- Escalated concerns: Executive Sponsor

**Stakeholder Management Activities:**

**Identification & Analysis:**
- [ ] Create stakeholder register
- [ ] Map stakeholder interests
- [ ] Assess power/influence
- [ ] Identify communication preferences

**Engagement:**
- [ ] Execute engagement plan
- [ ] Conduct regular reviews
- [ ] Gather feedback
- [ ] Address concerns

**Communication:**
- [ ] Status updates
- [ ] Change notifications
- [ ] Outcome communication
- [ ] Satisfaction surveys

---

## RACI Matrix by Process

### RACI Legend
- **R** = Responsible (executes task)
- **A** = Accountable (final authority, approval)
- **C** = Consulted (provides input)
- **I** = Informed (kept in the loop)

### Project Initiation

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Define project scope | A | C | I | C | I | R |
| Initial risk assessment | R | C | C | R | - | C |
| Identify stakeholders | C | - | - | - | - | A/R |
| Define communication plan | R | C | - | C | - | C |
| Approve project charter | A | - | - | - | - | C |

### Sprint Planning

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Refine user stories | C | I | C | C | - | I |
| Define acceptance criteria | C | R | R | R | - | C |
| Estimate effort | - | R | R | - | - | - |
| Identify dependencies | R | C | C | C | C | - |
| Plan testing approach | - | C | R | R | - | - |

### Development Phase

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Code review | - | R | I | R | - | - |
| Security code review | - | R | - | R | - | - |
| Define logging/monitoring | - | R | C | R | - | - |
| SAST/dependency scan | - | R | - | C | - | - |
| Document architecture | - | R | - | R | - | - |

### Testing Phase

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Define test cases | - | C | R | C | - | - |
| Security test cases | - | C | R | R | - | - |
| Execute tests | - | - | R | C | - | - |
| Triage defects | C | R | R | - | - | - |
| Performance testing | - | C | R | - | - | - |
| Security testing | - | - | R | R | - | - |

### Release & Deployment

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Quality gate | - | C | A | - | C | - |
| Security gate | - | - | - | A | C | - |
| Change approval | A | - | - | C | R | C |
| Deployment communication | C | - | - | - | R | A |
| Post-deployment validation | C | R | R | C | - | - |

### Change Management

| Activity | PM | Dev Lead | QA Lead | Security Champion | Change Control | Stakeholder Owner |
|----------|----|----|---------|------------------|---------|---------|
| Receive change request | C | - | - | - | R | - |
| Impact assessment | C | R | C | R | A | C |
| Approval routing | I | C | - | C | R | - |
| Communication | I | - | - | - | R | C |
| Implementation tracking | A | - | - | - | R | - |
| Stakeholder notification | I | - | - | - | C | A |

---

## Role Interactions & Communication

### Daily Communication Protocol

**Daily Standup (15 minutes)**
- **Participants:** PM, Dev Lead, QA Lead, Security Champion (if needed)
- **Topics:** Progress, blockers, risks
- **Owner:** Project Manager

**Issue Triage (as-needed)**
- **Participants:** PM, QA Lead, Development Team
- **Topics:** Defect assessment, priority, assignment
- **Owner:** QA Lead

### Weekly Communication Protocol

**Status Review (60 minutes)**
- **Participants:** PM, all leads, Product Owner
- **Topics:** Schedule, scope, quality, risks, issues
- **Deliverable:** Status report
- **Owner:** Project Manager

**Architecture Review (if needed)**
- **Participants:** Dev Lead, Security Champion, QA Lead
- **Topics:** Design decisions, security implications, testing approach
- **Owner:** Development Lead

**Change Management Review**
- **Participants:** PM, Change Control Coordinator, Dev Lead, Security Champion
- **Topics:** Pending changes, approvals, implementation status
- **Owner:** Change Control Coordinator

### Monthly Communication Protocol

**Executive Status**
- **Participants:** PM, Executive Sponsor
- **Topics:** Budget, schedule, risks, business value
- **Deliverable:** Executive summary report
- **Owner:** Project Manager

**Team Retrospective**
- **Participants:** All team members
- **Topics:** What went well, what to improve, actions
- **Owner:** Project Manager

---

## Accountability & Escalation

### Escalation Matrix

| Issue | Level 1 Owner | Level 2 Owner | Level 3 Owner |
|-------|---------------|---------------|---------------|
| **Schedule Delay** | Dev Lead | Project Manager | Executive Sponsor |
| **Scope Creep** | Product Owner | Project Manager | Executive Sponsor |
| **Budget Overrun** | Project Manager | CFO/Finance | Executive Sponsor |
| **Quality Risk** | QA Lead | Project Manager | CTO |
| **Security Risk** | Security Champion | CTO | CISO |
| **Stakeholder Issue** | Stakeholder Owner | Project Manager | Executive Sponsor |
| **Change Approval** | Change Coordinator | Project Manager | Executive Sponsor |
| **Technical Blocker** | Dev Lead | CTO | CTO |
| **Resource Conflict** | Project Manager | Executive Sponsor | C-Suite |

### Escalation Triggers

**IMMEDIATE (Same Day):**
- CRITICAL security vulnerability
- System outage/data loss risk
- Critical compliance violation
- Executive/customer escalation

**URGENT (Within 24 hours):**
- HIGH severity issue affecting release
- Budget significantly overrun
- Major stakeholder concern
- Significant schedule slip (>1 sprint)

**STANDARD (Within 1 week):**
- MEDIUM severity issue
- Process improvement needs
- Resource availability issues
- Minor scope changes

---

## Appendix: Role Readiness Checklist

### For Each Role Assignment, Verify:

```
ROLE: ________________________     PERSON: ________________________

READINESS CHECKLIST:
[ ] Role responsibilities understood
[ ] Authority levels defined
[ ] Required experience/skills verified
[ ] Stakeholders identified
[ ] Communication plan established
[ ] Escalation paths defined
[ ] Tools/systems access configured
[ ] Training/onboarding scheduled
[ ] Team introduction completed
[ ] First meeting scheduled

SIGNATURE: ________________________     DATE: ____________________
```

---

## References
- PMBOK (Project Management Body of Knowledge)
- ITIL Service Management
- Agile Manifesto & Practices
- OWASP Secure Development Framework