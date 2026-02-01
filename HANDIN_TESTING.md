# Risks and Assumptions

This chapter describes the key assumptions and potential risks related to testing the Börsibaar application.  
Its purpose is to identify dependencies, constraints and uncertainties that may affect testing activities, coverage and reliability.

---

## 1. Assumptions

The following assumptions are made to ensure effective testing of the Börsibaar application:

- Functional requirements, user stories and business rules (inventory management, pricing logic, POS flow) are sufficiently defined and remain stable during the testing phase.
- Backend and frontend components follow the agreed system architecture and API contracts.
- Test environments (local development, CI, future staging) are properly configured and accessible to all team members.
- Docker Compose provides a consistent setup for backend, frontend and PostgreSQL database testing.
- Test data can be reliably created using database seeding, Liquibase test changesets or predefined fixtures.
- OAuth2 authentication can be executed using test accounts or replaced with mock authentication during automated testing.
- JWT authorization rules and user roles are clearly defined and documented.
- CI/CD pipelines (GitHub Actions) are available to execute automated tests on every push and pull request.
- Testing tools and frameworks defined in the test plan are supported by the project configuration.
- External dependencies can be mocked or stubbed during automated testing when required.

---

## 2. Risks

The following risks may impact testing quality, coverage or delivery schedule:

### 2.1 Authentication Complexity Risk
OAuth2 authentication relies on external providers and redirect-based flows, which may cause instability in automated integration and end-to-end tests.

**Mitigation:**
- Use mock authentication in automated tests.
- Limit OAuth-based testing mainly to staging and manual testing.

---

### 2.2 Test Environment Inconsistency Risk
Differences between local, CI and staging environments (environment variables, CORS rules, redirect URLs) may result in inconsistent behavior.

**Mitigation:**
- Document environment configurations.
- Maintain shared `.env.example` files.
- Validate builds and tests in CI for every pull request.

---

### 2.3 Database Migration Risk
Liquibase schema changes may introduce migration failures, data inconsistencies or broken integrations.

**Mitigation:**
- Run migrations automatically in integration tests.
- Use Testcontainers to validate real PostgreSQL behavior.
- Review database changes during code reviews.

---

### 2.4 Flaky End-to-End Tests
UI-based automated tests may fail intermittently due to timing issues, animations or unstable selectors.

**Mitigation:**
- Use stable selectors (`data-testid`).
- Avoid testing visual details.
- Focus E2E tests on critical user flows only.
- When developing new features, check and update tests too.

---

### 2.5 Limited Time and Resources
Due to academic project constraints, full test coverage across all testing levels may not be achievable.

**Mitigation:**
- Apply risk-based testing.
- Prioritize critical flows (authentication, inventory, pricing, POS).
- Emphasize unit and integration testing over E2E volume.

---

### 2.6 Performance Degradation Risk
Inventory operations, pricing calculations or reporting endpoints may degrade under increased load.

**Mitigation:**
- Perform basic performance testing for critical endpoints.
- Monitor response times in CI or staging when possible.

---

### 2.7 Security Configuration Risk
Incorrect CORS rules, authorization logic or role restrictions may expose unauthorized access paths.

**Mitigation:**
- Add negative authorization test cases.
- Review security configuration regularly.
- Perform manual security checks for common vulnerabilities.

---

### 2.8 Rapid Feature Change Risk
Frequent feature changes may increase maintenance overhead for automated tests.

**Mitigation:**
- Follow the test pyramid model.
- Keep tests focused on business behavior rather than implementation details.
- Maintain automated regression testing in CI.

---

## 3. Summary

Risks and assumptions provide visibility into factors that may affect testing effectiveness and system quality.  
By identifying these areas early, the testing process can focus on high-risk components, ensure realistic expectations and support stable project delivery.

# Test Deliverables

This chapter describes all testing-related deliverables produced during the Börsibaar project testing lifecycle.  
Test deliverables represent tangible outputs of testing activities and provide visibility into test coverage, quality status and system readiness.

---

## 1. Documentation Deliverables

The following documentation artifacts will be created and maintained:

- **Test Plan**
    - Defines testing scope, objectives, approach, environments, roles, risks and assumptions.

- **Test Scenarios**
    - High-level descriptions of user flows and system behaviors to be validated.

- **Test Cases**
    - Detailed test steps with expected results for unit, integration, system and user-flow testing.

- **Smoke Test Checklist**
    - List of critical checks executed after deployments to validate system availability.

- **Test Summary Report**
    - Overview of executed tests, results, known defects and remaining risks.

---

## 2. Automated Testing Deliverables

### 2.1 Backend Testing Artifacts
- Unit test suite implemented using **JUnit 5** and **Mockito**.
- Integration tests using **Spring Boot Test** and **Testcontainers**.
- REST API and controller tests using **MockMvc** or **WebTestClient**.
- Database migration verification tests for **Liquibase**.
- Test execution and result logs.

---

### 2.2 Frontend Testing Artifacts
- Unit and component tests using **Jest** and **React Testing Library**.
- Integration tests for frontend-backend communication.
- Next.js API route tests with mocked services.
- Mock definitions using **MSW (Mock Service Worker)**.
- Test result reports and coverage output.

---

### 2.3 End-to-End Testing Artifacts
- Automated E2E test suites implemented using **Cypress**.
- Test scenarios covering critical user journeys:
    - Authentication and authorization flow
    - Dashboard access
    - Inventory management
    - POS operations
    - Public pricing view
- Cross-browser validation results (if applicable).
- Screenshots and video recordings generated during test runs.

---

## 3. CI/CD and Quality Deliverables

The following deliverables are generated automatically through the CI/CD pipeline:

- **Automated test execution reports** from GitHub Actions.
- **Build verification results** for backend and frontend services.
- **Code coverage reports**:
    - Backend: JaCoCo XML and HTML reports.
    - Frontend: Jest coverage (LCOV format).
- **Static code analysis reports** from SonarQube.
- **Quality gate status reports** indicating pass or failure conditions.
- - **Lighthouse CI reports** (performance, accessibility, best practices, SEO) generated during CI runs (if configured).

---

## 4. Performance and Reliability Deliverables

If performance testing is executed, the following artifacts may be produced:

- Load test scripts (k6, JMeter, Artillery).
- Performance metrics reports:
    - API response times
    - Throughput
    - Error rates
- Frontend performance metrics:
    - Lighthouse scores
    - Web Vitals measurements.

---

## 5. Defect Management Deliverables

- **Bug reports** containing:
    - Description of the issue
    - Reproduction steps
    - Expected and actual results
    - Severity and priority
    - Logs, screenshots or videos

- **Defect verification records**
    - Confirmation of fixes.
    - Regression test evidence.

- **Known issues list**
    - Open defects at the end of testing.

---

## 6. Final Testing Outputs

At the conclusion of the testing phase, the following final deliverables will be available:

- Completed automated test suites.
- Final test execution results.
- Test summary report.
- List of unresolved risks and known limitations.
- Recommendation regarding system readiness for demonstration or release.

---

## 7. Summary

Test deliverables provide measurable evidence of testing activities and system quality.  
They ensure transparency, traceability and confidence in the stability, security and correctness of the Börsibaar application.
