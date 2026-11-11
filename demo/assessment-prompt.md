# Contoso University modernization assessment prompt

Run this prompt from a dedicated throwaway demo branch, not from `main`.

```text
Assess Contoso University for modernization. Do not implement the migration yet.

Target platform:
- .NET 10 and ASP.NET Core 10
- Azure Container Apps, preferably Linux containers
- Azure SQL Database
- Azure Container Registry
- Azure Monitor Application Insights
- Microsoft Entra ID
- Azure Key Vault
- Assess whether Azure Blob Storage and Azure Service Bus are required
  to replace local uploads and MSMQ.

Scope and safeguards:
- Work only on the current throwaway demo branch.
- Never merge into main, open a pull request, or enable auto-merge.
- Application code must remain unchanged during assessment.
- Creating or updating assessment documents and diagrams is permitted.
- Do not provision resources, deploy, modify databases, or incur Azure costs.
- Never include secrets, connection-string values, or personal data in outputs.

Inspect the actual implementation, configuration, dependency manifests,
database mappings, and existing documentation. Treat documentation as
potentially outdated. Cite repository paths and line numbers for findings.
Clearly distinguish verified facts, assumptions, and unknowns.

Produce an assessment organized into these sections:

1. Issues
   Identify modernization blockers, unsupported dependencies, Windows/IIS
   coupling, security concerns, and operational risks. For each finding,
   include evidence, impact, priority, recommended remediation, and
   dependencies on other work.

   Assess known vulnerabilities in direct and transitive NuGet packages
   and bundled JavaScript libraries. Include container base images only
   if they already exist. Use current authoritative advisory sources,
   recording the assessment date, installed version, advisory/CVE ID,
   severity, affected range, fixed version, source URL, and application
   relevance. Distinguish confirmed vulnerable versions from unverified
   exposure. Report unsupported components separately from CVEs.
   State scan limitations; never interpret missing results as no CVEs.

2. Architecture
   Document the current application components, hosting assumptions,
   external dependencies, trust boundaries, and data flows.
   Create an evidence-based current-state Mermaid architecture diagram.
   Do not depict proposed Azure services as already implemented.
   Separately create a proposed Azure target-state diagram and explain
   the mapping from current components to target services.

3. API Contracts
   Inventory actual MVC routes, HTTP endpoints, methods, authorization,
   inputs, outputs, validation, and error behavior. Distinguish rendered
   HTML actions from JSON APIs; do not invent REST APIs or OpenAPI contracts.
   Identify compatibility requirements for existing callers and UI flows.

4. Configuration
   Document configuration keys and their purpose, source, environment
   differences, and sensitivity without exposing values.
   Assess migration from Web.config and IIS settings to ASP.NET Core
   configuration, environment variables, managed identities, and Key Vault.

5. Business Workflows
   Document implemented workflows for students, enrollment, courses,
   instructors, departments, teaching-material uploads, and notifications.
   Include permissions, validation, failure paths, and external dependencies.
   Create sequence diagrams for the most important cross-component flows.

6. Dependencies
   Inventory frameworks, NuGet packages, bundled frontend libraries,
   native dependencies, Windows services, and external systems.
   Identify replacements, supported target versions, breaking changes,
   licensing concerns, and migration effort.
   Verify version recommendations against current official sources.

7. Data Model
   Document entities, relationships, keys, constraints, delete behavior,
   concurrency handling, initialization/seeding, and migration mechanisms.
   Create a current-state Mermaid ER diagram based on implemented mappings.
   Assess Azure SQL compatibility, data preservation, migration validation,
   backup/restore, and rollback. Flag destructive startup initialization.

Cross-cutting assessment:
- Windows authentication to Entra ID, including existing role semantics.
- Managed-identity access to SQL, ACR, Key Vault, and other Azure services.
- Container readiness: filesystem persistence, session state, Data Protection
  keys, native dependencies, ports, forwarded headers, health probes,
  graceful shutdown, scaling, and cold starts.
- Upload durability and security; messaging retries and idempotency.
- Structured logging, distributed tracing, correlation, alerts, and PII hygiene.
- Network exposure, least privilege, secret rotation, and environment isolation.
- Existing test coverage and characterization tests needed to preserve behavior.
- CI/CD, infrastructure as code, image scanning, and deployment rollback.
- Indicative Azure cost drivers and demo resource cleanup.

Deliverables:
- A concise executive summary with readiness, blockers, and key decisions.
- Updated current-state application documentation in docs, with a clear index.
- Current-state architecture and ER diagrams, plus a separate target diagram.
- A prioritized modernization backlog with acceptance criteria and a
  dependency-ordered migration plan.
- A short live-demo path, clearly separated from production-hardening work.

Keep the proposed design simple. Preserve business behavior and avoid
unnecessary microservices or new infrastructure. End with unresolved
decisions requiring my approval, and stop before implementation.
```

## Live-demo preparation

Prepare reproducible sample data, a known-good starting point, and a reset path.
Rehearse authentication setup, Azure permissions, and container cold starts.
