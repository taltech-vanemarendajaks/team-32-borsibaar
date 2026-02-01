# Test Approach

This chapter defines the overall testing strategy, approach and principles for the Börsibaar project. It describes testing levels, selection criteria and quality and performance testing implementation.

---

## 1 Overall Testing Strategy

The Börsibaar project follows the **Test Pyramid model** as a guideline for efficient testing:

- **70% Unit Tests**: Focused on fast feedback and testing individual components.
- **20% Integration Tests**: Validating collaboration between components.
- **10% End-to-End Tests**: Ensuring the application works as expected from the user's perspective.

These ratios are target values and may evolve as the system grows. The pyramid is also used as a **risk-escalation model**, where defects should be detected as early and as close to the source as possible.

## 2 How Testing Levels Are Applied

Testing levels described in *Testing levels* are applied progressively based on feedback speed, risk, and change scope:

* Unit tests act as the primary quality gate for development work and are expected to run frequently.
* Integration tests (including API tests) validate system boundaries such as databases, migrations, and security constraints before changes are considered deployable.
* Frontend component tests focus on UI behavior, validation logic, and predictable state transitions.
* End-to-end tests are intentionally limited to critical business flows that span multiple system components.
* Manual and exploratory testing complements automation in areas with high usability or requirement uncertainty.

**End-to-end tests are used primarily as confidence-building checks for critical business flows and are not intended to replace unit or integration tests, in order to keep the test suite maintainable and execution times reasonable.**

## 3 Test Selection Rules

To avoid duplicated coverage and excessive maintenance effort, tests are selected according to the following principles:

* Business rules and calculations are verified using unit tests.
* Persistence behavior, migrations, and transactional consistency are covered by integration tests.
* Authentication, authorization, and API contracts are validated via API tests.
* UI validation and client-side logic are verified through frontend component tests.
* Cross-cutting user journeys are validated using end-to-end tests.
* Usability, layout, and edge cases are explored through manual testing.

## 4 Entry and Exit Criteria

**Entry criteria:**

* Feature implementation completed and code reviewed.
* Relevant unit tests implemented.
* Required test data strategy defined.

**Exit criteria:**

* CI pipeline completed successfully according to branch policy.
* No unresolved critical or high-severity defects.
* Coverage and static analysis thresholds met.
* Smoke testing passed in the relevant environment.

*Final release readiness decisions are made jointly by the Test Lead and Product Owner based on risk assessment and business requirements.*

## 5 Test Automation and Execution Policy

Automated testing is integrated into the CI/CD pipeline to ensure continuous feedback:

* Every push triggers fast automated checks.
* Pull requests and main branch builds execute extended test suites including E2E tests.
* Before major releases, selected non-functional tests are executed for critical flows.

## 6 Non-Functional Testing Strategy

Non-functional testing is applied selectively and risk-based:

* Performance testing focuses on critical APIs and user journeys.
* Stability testing targets previously unstable or failure-prone areas.
* Basic security checks are performed in non-production environments.

### 6.1 Quality Metrics and Performance Criteria

**Code Coverage Targets:**
- Backend: Minimum 80% line coverage.
- Frontend: Minimum 80% line coverage.
- Critical Paths: 85% coverage target.

**Performance Criteria:**
- API Response Time: < 500ms (95th percentile) for critical endpoints.
- Page Load Time: < 5 seconds for main user interfaces.
- Database Queries: < 200ms average execution time.
- Authentication Flow: < 1000ms for complete OAuth2 workflow.

**Security Boundaries:**
- Input validation on all user-facing endpoints.
- SQL injection protection via parameterized queries.
- XSS prevention through proper output encoding.
- Authorization checks on all protected resources.

**Stability Thresholds:**
- System uptime: > 95% during testing periods.
- Memory usage: < 85% of allocated resources under normal load.
- Error rate: < 2% for critical business flows.

## 7 Traceability and Reporting

Testing results support release and quality decisions:

* Acceptance criteria are traceable to tests at appropriate levels.
* Test reports highlight coverage of critical paths and detected risks.
* Failures are categorized by impact to support prioritization and decision-making.

# Roles and Responsibilities

This chapter describes the testing team structure and responsibilities of each member in the Börsibaar project. It defines roles, required skills and technical responsibilities to ensure quality testing.

---

## 1 Testing Team Structure

The Börsibaar project testing team consists of 5 specialists, each with clearly defined responsibilities to ensure the quality, reliability, and maintainability of the application.

### 1.1 Test Lead (1 person)

**Primary Responsibilities:**

* Define and maintain the overall testing strategy.
* Plan, coordinate, and prioritize testing activities across teams.
* Ensure testing aligns with business and technical requirements.
* Communicate testing status, risks, and results to stakeholders.
* Review and approve test plans and test cases.
* Produce and present test reports and quality metrics.

**Required Skills:**

* Strong knowledge of software testing methodologies and best practices.
* Experience with project coordination and risk management.
* Solid technical background (frontend and backend awareness).

### 1.2 Backend Test Engineer (1 person)

**Primary Responsibilities:**

* Unit testing of the Spring Boot backend application.
* API integration testing for REST endpoints.
* Database integration testing with PostgreSQL.
* JWT authentication and OAuth2 (Google) flow testing.
* Service and repository layer validation.
* Liquibase migration testing.

**Technical Responsibilities:**

* Maintain backend tests under the dedicated test directory.
* Use JUnit 5 and Spring Boot Test.
* Use Testcontainers with PostgreSQL for integration tests.
* Create mocks and stubs using Mockito.

### 1.3 Frontend Test Engineer (1 person)

**Primary Responsibilities:**

* Unit testing of React components in Next.js with TypeScript.
* Testing Next.js API routes.
* UI integration testing.
* Validation of frontend–backend communication.
* Testing custom hooks and utility functions.

**Technical Responsibilities:**

* Use Jest and React Testing Library.
* Mock APIs using MSW (Mock Service Worker).
* Validate component rendering, user interactions, and state changes.
* Ensure TypeScript compile-time correctness via CI checks.

### 1.4 End-to-End & Non-Functional Test Engineer (1 person)

**Primary Responsibilities:**

* Automation of complete end-user scenarios.
* Cross-browser compatibility testing.
* Mobile responsiveness testing.
* Coordination and execution of non-functional tests (performance, stability).
* Support integration testing across system boundaries.

**Technical Responsibilities:**

* Create and maintain Cypress E2E test suites.
* Manage test environments using Docker Compose.
* Integrate E2E tests into the CI/CD pipeline.
* Execute and analyze performance and load tests.

### 1.5 Manual Test Engineer (1 person)

**Primary Responsibilities:**

* Exploratory testing of new and high-risk features.
* Usability and user experience validation.
* Basic security sanity checks in non-production environments.
* Bug reporting, verification, and regression testing.
* Smoke testing after deployments.
* Coordination of User Acceptance Testing (UAT).

**Technical Responsibilities:**

* Documentation of manual test cases and scenarios.
* Usage of bug tracking and test management tools.
* Collaboration with product owners and stakeholders during UAT.


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
