# OctoACME QA Standards & Acceptance Criteria

**Document Purpose:** Define quality assurance protocols, testing standards, and acceptance criteria to ensure consistent delivery of high-quality, secure software.

**Owner:** QA Lead  
**Stakeholders:** Project Manager, Development Lead, Security Champion, Product Owner  
**Last Updated:** 2026-05-02

---

## Table of Contents
1. [QA Governance](#qa-governance)
2. [Quality Definition & Metrics](#quality-definition--metrics)
3. [Acceptance Criteria Standards](#acceptance-criteria-standards)
4. [Testing Strategy by Phase](#testing-strategy-by-phase)
5. [Defect Management](#defect-management)
6. [QA Lead Responsibilities](#qa-lead-responsibilities)
7. [Test Case Documentation](#test-case-documentation)
8. [Quality Assurance Checklist](#quality-assurance-checklist)

---

## QA Governance

### Quality Principles
- **Shift-Left Testing:** Test early in development, not just at the end
- **Continuous Quality:** Quality is embedded in every phase, not a final gate
- **Acceptance-Driven:** All deliverables must meet predefined acceptance criteria
- **Risk-Based Testing:** Focus testing effort on high-risk areas
- **Automation-First:** Automate repetitive tests; reserve manual testing for exploratory scenarios
- **Traceability:** Every test traces back to a requirement or user story

### RACI for Quality Decisions
| Role | Responsibility |
|------|-----------------|
| **QA Lead** | Responsible & Accountable for QA strategy, testing execution, and acceptance |
| **Development Lead** | Responsible for test automation; Consulted on testability |
| **Security Champion** | Consulted on security testing requirements |
| **Product Owner** | Accountable for acceptance criteria definition |
| **Project Manager** | Informed of quality metrics and schedule impacts |

---

## Quality Definition & Metrics

### Definition of Done (DoD)

A user story or feature is "Done" when:

- [ ] **Functional Requirements Met**
  - All acceptance criteria satisfied
  - Feature behaves as documented
  - Edge cases handled gracefully

- [ ] **Code Quality Standards**
  - Code review approved (peer review + security review spot-checks)
  - SAST findings resolved or documented
  - Code coverage ≥ 80% for critical paths
  - No duplicate code or complexity violations

- [ ] **Security Requirements Met**
  - Security acceptance criteria satisfied
  - OWASP Top 10 vulnerabilities tested for
  - Secrets and credentials not hardcoded
  - Authentication/authorization flows validated

- [ ] **Performance Standards**
  - Response times meet SLA targets
  - No memory leaks or resource exhaustion
  - Load testing completed (for user-facing features)

- [ ] **Testing Complete**
  - Unit tests written and passing (>80% coverage)
  - Integration tests passing
  - Acceptance tests passing
  - Security tests passing
  - Manual test cases executed and documented

- [ ] **Documentation**
  - Code comments for complex logic
  - API documentation updated (if applicable)
  - User documentation updated
  - Known limitations documented

- [ ] **Deployment Readiness**
  - Database migrations tested (if applicable)
  - Rollback plan defined
  - Monitoring and alerting configured
  - No blocking defects

### Key Quality Metrics

| Metric | Target | Owner |
|--------|--------|-------|
| **Code Coverage** | ≥80% for critical paths | Development Lead |
| **Defect Escape Rate** | <5% (production defects vs. total defects) | QA Lead |
| **Mean Time to Resolution (MTTR)** | CRITICAL: <1 hour, HIGH: <24 hours | QA Lead |
| **Test Automation Rate** | ≥70% of test cases automated | QA Lead |
| **Security Vulnerability Escape Rate** | 0% CRITICAL/HIGH findings post-release | Security Champion |

---

## Acceptance Criteria Standards

### What are Acceptance Criteria?

Acceptance Criteria (AC) are **specific, measurable conditions** that a user story must satisfy to be considered complete and accepted.

### Acceptance Criteria Template

```
USER STORY: [As a {role}, I want to {capability}, so that {benefit}]

ACCEPTANCE CRITERIA:

Given: [Initial state/context]
When: [Action performed]
Then: [Expected result]

SECURITY ACCEPTANCE CRITERIA (if applicable):
- [ ] [Security-specific acceptance criterion]

PERFORMANCE ACCEPTANCE CRITERIA (if applicable):
- [ ] [Performance-specific acceptance criterion]

EDGE CASES:
- [ ] [Edge case 1]
- [ ] [Edge case 2]

ACCEPTANCE SIGN-OFF:
Approved By: ________________________     Date: ____________________
```

### Acceptance Criteria Best Practices

✅ **DO:**
- Write criteria in Gherkin format (Given/When/Then)
- Be specific and measurable
- Include security and performance criteria
- Cover happy path, sad path, and edge cases
- Involve Product Owner, Development Lead, and QA Lead
- Document assumptions and dependencies

❌ **DON'T:**
- Use vague language ("should be fast", "should be easy")
- Create overly complex scenarios
- Forget edge cases and error conditions
- Neglect security considerations
- Leave criteria ambiguous for interpretation

### Acceptance Criteria Checklist

Before marking a story as "Ready for Dev":
- [ ] Acceptance criteria are written in Gherkin (Given/When/Then)
- [ ] Criteria are specific and measurable
- [ ] Criteria are testable (can verify pass/fail)
- [ ] Security criteria are included (if applicable)
- [ ] Performance criteria are included (if applicable)
- [ ] Edge cases are documented
- [ ] Dependencies are identified
- [ ] Accepted by Product Owner, Dev Lead, QA Lead

---

## Testing Strategy by Phase

### Phase 1: Unit Testing (Developer Responsibility)

**When:** During development  
**Owner:** Development Team  
**Tools:** JUnit, Jest, PyTest, RSpec (language-dependent)

**Standards:**
- Minimum 80% code coverage for critical paths
- All public methods have test cases
- Edge cases and error conditions tested
- Tests are automated and run in CI/CD pipeline
- Tests pass before code review

**Criteria for Acceptance:**
- [ ] Unit tests written for all new code
- [ ] Coverage ≥80% for critical paths
- [ ] All tests passing locally and in CI
- [ ] Peer code review approved

---

### Phase 2: Integration Testing (QA + Dev Responsibility)

**When:** After unit testing, during development sprint  
**Owner:** QA Lead + Development Lead  
**Focus:** Interactions between components, APIs, databases

**Standards:**
- Test API contracts (request/response validation)
- Test database transactions (ACID properties)
- Test inter-service communication (if microservices)
- Test data flow end-to-end

**Test Cases:**
- [ ] Positive scenarios (happy path)
- [ ] Negative scenarios (error handling)
- [ ] Boundary conditions (min/max values)
- [ ] Authentication/Authorization boundaries
- [ ] Data validation (type, format, constraints)

**Criteria for Acceptance:**
- [ ] Integration tests written and automated
- [ ] Tests pass in staging environment
- [ ] No data integrity issues
- [ ] Error handling validated

---

### Phase 3: Functional Testing (QA Lead Responsibility)

**When:** After development complete, before release  
**Owner:** QA Lead  
**Focus:** Feature behavior against requirements

**Test Coverage:**
- [ ] All acceptance criteria validated
- [ ] All user workflows tested
- [ ] All business rules enforced
- [ ] UI/UX consistency checked
- [ ] Localization tested (if multi-language)

**Manual Testing Focus Areas:**
- Complex workflows that are difficult to automate
- User experience and usability
- Accessibility (keyboard navigation, screen readers)
- Cross-browser/platform compatibility (if applicable)

**Criteria for Acceptance:**
- [ ] All acceptance criteria passing
- [ ] No blocking defects
- [ ] User workflows validated
- [ ] QA Lead sign-off obtained

---

### Phase 4: Security Testing (QA Lead + Security Champion)

**When:** During execution phase, before release  
**Owner:** QA Lead + Security Champion  
**Reference:** `octoacme-security-compliance-checklist.md`

**Security Test Coverage:**
- [ ] OWASP Top 10 (2025) test cases
- [ ] Injection attacks (SQL, NoSQL, Command)
- [ ] Authentication brute force, session hijacking
- [ ] Authorization bypass attempts
- [ ] Sensitive data exposure
- [ ] Cryptographic validation
- [ ] File upload validation (if applicable)
- [ ] CSRF/CORS vulnerabilities (if applicable)

**Tools:**
- DAST: OWASP ZAP, Burp Suite Community
- SAST: Already covered in development phase
- Fuzzing: AFL, libFuzzer (if applicable)

**Criteria for Acceptance:**
- [ ] No CRITICAL security findings
- [ ] All HIGH findings have remediation plan
- [ ] Security test cases documented
- [ ] Security Champion sign-off obtained

---

### Phase 5: Performance Testing (QA Lead)

**When:** Before release (especially for user-facing or backend services)  
**Owner:** QA Lead  
**Focus:** Response times, throughput, scalability

**Performance Test Scenarios:**
- [ ] Load test: Simulate expected concurrent users
- [ ] Stress test: Identify breaking point
- [ ] Spike test: Sudden increase in load
- [ ] Soak test: Extended period at high load

**Performance Acceptance Criteria:**
- [ ] Response time: <500ms for user-facing, <1s for complex queries
- [ ] Throughput: ≥[X] requests/second (define per service)
- [ ] Memory: No leaks, stable over time
- [ ] CPU: <85% under peak load

**Tools:**
- JMeter, Gatling, Locust, k6

**Criteria for Acceptance:**
- [ ] Performance tests executed
- [ ] Results meet SLA targets
- [ ] Bottlenecks identified and addressed

---

### Phase 6: Smoke Testing (QA Lead)

**When:** After deployment to production  
**Owner:** QA Lead + Operations  
**Focus:** Critical path validation in production

**Smoke Test Coverage:**
- [ ] Application starts without errors
- [ ] Critical user workflows function
- [ ] Database connectivity verified
- [ ] Essential third-party integrations operational
- [ ] Monitoring and alerts active

**Criteria for Acceptance:**
- [ ] All smoke tests passing
- [ ] No critical issues post-deployment
- [ ] Ready for broader user access

---

## Defect Management

### Defect Severity Classification

| Severity | Definition | MTTR Target | Impact |
|----------|-----------|-------------|--------|
| **CRITICAL** | System down, data loss, security breach | <1 hour | Blocks production |
| **HIGH** | Major feature unavailable, severe issue | <24 hours | Significant impact on users |
| **MEDIUM** | Feature partially working, moderate issue | <3 days | Workaround exists |
| **LOW** | Minor issue, cosmetic, no workaround needed | <2 weeks | Minimal user impact |
| **INFORMATIONAL** | Observation, suggestion, best practice | No target | No impact; FYI only |

### Defect Lifecycle

```
NEW → ASSIGNED → IN PROGRESS → TESTING → VERIFIED FIXED / REOPENED → CLOSED
```

### Defect Reporting Template

```
DEFECT ID: ____________________     SEVERITY: ☐ CRITICAL ☐ HIGH ☐ MEDIUM ☐ LOW ☐ INFO

TITLE: _________________________________________________________________

ENVIRONMENT: [ ] Development  [ ] Staging  [ ] Production
OS/BROWSER: ________________________     DEVICE: ____________________

STEPS TO REPRODUCE:
1. ________________________________________
2. ________________________________________
3. ________________________________________

EXPECTED RESULT:
_________________________________________________________________

ACTUAL RESULT:
_________________________________________________________________

ATTACHMENTS:
[ ] Screenshot   [ ] Video   [ ] Log files   [ ] Test data

SECURITY IMPACT: [ ] None  [ ] Potential  [ ] Confirmed
If applicable, notify Security Champion: _____ (yes/no)

REPORTED BY: ________________________     DATE: ____________________
ASSIGNED TO: ________________________     DUE DATE: ____________________
```

### Escalation Triggers

| Condition | Action |
|-----------|--------|
| CRITICAL defect in production | Immediate escalation to Project Manager, CTO |
| CRITICAL defect impacts security | Escalate to Security Champion + CTO |
| HIGH defect blocks release | Escalate to Project Manager for prioritization |
| Defect MTTR exceeded | Escalate to Development Lead |

---

## QA Lead Responsibilities

### Core Accountabilities
1. **Test Strategy:** Define comprehensive testing approach for each phase
2. **Test Execution:** Execute and automate test cases
3. **Quality Gate:** Approve feature/release readiness
4. **Defect Triage:** Assess severity and assign for resolution
5. **Escalation:** Identify and escalate quality risks
6. **Metrics:** Track and report quality metrics
7. **Team Development:** Coach team on testing best practices

### Key Interactions
- **With Product Owner:** Clarify acceptance criteria
- **With Development Lead:** Understand architecture; define testability requirements
- **With Security Champion:** Incorporate security test cases
- **With Project Manager:** Report quality status and schedule impacts

### Weekly Responsibilities
- [ ] Triage new defects
- [ ] Review test execution progress
- [ ] Update quality metrics
- [ ] Escalate any quality risks
- [ ] Coordinate security testing (if applicable)

### Pre-Release Responsibilities
- [ ] Comprehensive test execution complete
- [ ] All acceptance criteria validated
- [ ] Security testing complete
- [ ] Performance testing complete (if applicable)
- [ ] Release readiness sign-off

---

## Test Case Documentation

### Test Case Template

```
TEST CASE ID: TC-001     PROJECT: [Project Name]     VERSION: 1.0

TITLE: [Clear, descriptive test case title]

OBJECTIVE: [What is being tested and why]

PREREQUISITES:
- [ ] System is running
- [ ] User is logged in
- [ ] Test data is prepared

TEST STEPS:
Step 1: [First action] | Expected: [Expected result]
Step 2: [Second action] | Expected: [Expected result]
Step 3: [Third action] | Expected: [Expected result]

EXPECTED RESULT: [Overall expected outcome]

ACTUAL RESULT: _______________________________________________

STATUS: [ ] PASS  [ ] FAIL  [ ] BLOCKED

DEFECTS FOUND (if any):
- Defect ID: ____________
- Defect ID: ____________

EXECUTED BY: ________________________     DATE: ____________________
REVIEWED BY: ________________________     DATE: ____________________
```

### Test Case Best Practices

✅ **DO:**
- Write test cases in clear, step-by-step language
- Include prerequisites and setup steps
- Specify expected results explicitly
- Cover positive, negative, and edge cases
- Keep test cases focused and independent
- Use data-driven testing for multiple scenarios
- Maintain test cases as requirements evolve

❌ **DON'T:**
- Create dependent test cases (avoid order dependencies)
- Use vague language ("should work", "looks good")
- Forget to document expected results
- Create test cases too long or complex
- Neglect edge cases and error conditions

---

## Quality Assurance Checklist

### Pre-Development
- [ ] Acceptance criteria clearly defined and approved
- [ ] Test strategy documented
- [ ] Test data prepared
- [ ] Testing tools and environments ready
- [ ] QA team has requirements clarity

### During Development
- [ ] Unit tests written (80%+ coverage)
- [ ] Integration tests passing
- [ ] Code review completed
- [ ] SAST findings resolved
- [ ] Development environment testing successful

### Pre-Release
- [ ] Functional testing complete
- [ ] Security testing complete
- [ ] Performance testing complete (if applicable)
- [ ] All acceptance criteria validated
- [ ] No blocking defects
- [ ] Test execution documented
- [ ] Defects below threshold (≤1 CRITICAL, ≤3 HIGH)
- [ ] QA Lead release sign-off obtained

### Post-Release
- [ ] Smoke testing passed in production
- [ ] Production monitoring confirmed operational
- [ ] Incident response plan activated (if needed)
- [ ] Post-release testing documentation archived
- [ ] Lessons learned captured

---

## References
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [ISTQB Testing Certification](https://www.istqb.org/)
- [Gherkin Language Guide](https://cucumber.io/docs/gherkin/)
- [Test Automation Best Practices](https://github.com/dvabuya/test-automation-best-practices)