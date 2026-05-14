# Contoso University - GitHub Copilot App Modernization for .NET Demo

This repository contains the Contoso University sample application used to demonstrate **GitHub Copilot app modernization for .NET** in both **Visual Studio Code** and **Visual Studio**.

The demo follows the Microsoft Learn app modernization quickstarts and uses a legacy .NET Framework web application to show how GitHub Copilot can assess modernization readiness, create a migration plan, update code, validate builds, and help move Windows-oriented dependencies to Azure services.

## Demo Scenario

Contoso University is a fictional university management system built with .NET Framework 4.8. The application includes common line-of-business features such as:

- Student enrollment and profile management
- Course catalog management
- Instructor assignments and office locations
- Department administration
- Teaching material uploads
- Notification messaging

The legacy application uses Windows-based and local development dependencies that are common in older .NET applications:

- **SQL Server LocalDB** for database storage
- **Local file system** access for uploaded teaching materials
- **Microsoft Message Queue (MSMQ)** for notification messaging

During the modernization demo, GitHub Copilot can identify and help migrate these patterns to Azure-native services:

- **Azure SQL Database** instead of SQL Server LocalDB
- **Azure Blob Storage** instead of local file system storage
- **Azure Service Bus** instead of MSMQ
- **Azure Key Vault** for secure secrets management

## Microsoft Learn References

This README is based on the following Microsoft Learn guidance:

- [Contoso University migration sample](https://learn.microsoft.com/en-us/dotnet/azure/migration/appmod/sample)
- [Quickstart for Visual Studio Code](https://learn.microsoft.com/en-us/dotnet/azure/migration/appmod/quickstart?pivots=vscode)
- [Quickstart for Visual Studio](https://learn.microsoft.com/en-us/dotnet/azure/migration/appmod/quickstart?pivots=visualstudio)

## Prerequisites

### Required for both demo paths

- A GitHub account with access to GitHub Copilot
- This repository cloned locally
- A .NET development environment that can build and test the project
- Azure access for provisioning target services during migration tasks

### Visual Studio Code path

- [Visual Studio Code](https://code.visualstudio.com/) version 1.101 or later
- [GitHub Copilot in Visual Studio Code](https://code.visualstudio.com/docs/copilot/overview), signed in with your GitHub account
- [GitHub Copilot modernization extension](https://marketplace.visualstudio.com/items?itemName=vscjava.migrate-java-to-azure)
- Restart Visual Studio Code after installing the modernization extension

### Visual Studio path

- Windows operating system
- [Visual Studio 2026](https://visualstudio.microsoft.com/downloads/) or Visual Studio 2022 version 17.14.17 or later
- **.NET desktop development** workload with these optional components enabled:
  - GitHub Copilot
  - GitHub Copilot modernization agent
- Sign in to Visual Studio with a GitHub account that has Copilot access

If you change Copilot subscriptions or accounts, restart Visual Studio before running the demo.

## Open the Sample

Clone this repository and open the solution:

```bash
git clone <this-repository-url>
cd ghcp-appmod-net-university
```

For Visual Studio, open `ContosoUniversity.sln`.

For Visual Studio Code, open the repository folder and make sure the solution and project files are visible in the Explorer.

## Demo Flow

Use this flow for either IDE:

1. Run a modernization assessment.
2. Review the assessment report and recommended migration tasks.
3. Start a migration task from the report, task list, or chat.
4. Let GitHub Copilot generate the migration plan and progress tracker.
5. Review or edit the plan before code remediation begins.
6. Continue the migration so Copilot can update dependencies, configuration, and code.
7. Allow Copilot to build, validate, and fix issues until the project succeeds.
8. Review the final changes and keep the completed migration work.

Good demo migration tasks for this sample include:

- Migrating local file system storage for teaching materials to Azure Blob Storage
- Migrating SQL Server LocalDB usage to Azure SQL Database
- Migrating MSMQ notification messaging to Azure Service Bus
- Moving secrets and connection strings to Azure Key Vault

## Run the Demo in Visual Studio Code

### Assess the application

1. Open this repository in Visual Studio Code.
2. Open the **GitHub Copilot modernization** extension.
3. In the **QUICKSTART** section, select **Start Assessment**.
4. On the **Assessment reports** page, select **Run Assessment**.
5. Wait for the assessment to analyze the project and generate the report.

The report shows migration readiness findings and recommended modernization tasks.

### Start a chat-based migration

Chat-based migration is the recommended flow in Visual Studio Code.

1. Open GitHub Copilot Chat from the Activity Bar.
2. In the agent selector, choose **AppModernization-DotNet**.
3. Enter a modernization prompt using this pattern:

   ```text
   migrate from <source technology> to <target technology>
   ```

   Example prompts for this repository:

   ```text
   migrate from local file system to Azure Blob Storage
   ```

   ```text
   migrate from MSMQ to Azure Service Bus
   ```

4. Review the generated migration plan.
5. Enter or select **Continue** when you are ready for Copilot to make code changes.
6. Select **Keep** to accept the completed changes after the migration summary is generated.

### Start a migration from the UI

You can also start migration work from the modernization extension UI:

- Select **Run Task** from an assessment report finding.
- Run a predefined task from the **TASKS - .NET** section.

In Visual Studio Code, migration artifacts are created under:

```text
.github/appmod/code-migration/<target-branch-name>/
```

The key generated files are:

- `plan.md`: the migration plan
- `progress.md`: the migration progress tracker

## Run the Demo in Visual Studio

### Assess the application

1. Open `ContosoUniversity.sln` in Visual Studio.
2. In Solution Explorer, right-click the solution node.
3. Select **Modernize**.
4. In GitHub Copilot Chat, select **Migrate to Azure** and send it to Copilot.

You can also open GitHub Copilot Chat directly and send:

```text
@Modernize Migrate to Azure
```

Copilot starts a new modernization chat session, assesses the project, and displays an assessment report with recommended migration tasks.

### Start a migration task

Start migration in either of these ways:

- Select **Run Task** from the assessment report.
- Send a migration task number or migration task name in Copilot Chat.

For example, use the **File System Management** task to demonstrate migration from local file storage to Azure Blob Storage:

![Run migration task](media/run-migartion-task.png)

When migration starts, Visual Studio creates migration artifacts under:

```text
.appmod/.migration/
```

The key generated files are:

- `plan.md`: the migration plan
- `progress.md`: the migration progress tracker

After reviewing the generated plan, continue with a prompt such as:

```text
The plan and progress tracker look good to me. Go ahead with the migration.
```

## What GitHub Copilot Does During Migration

During code remediation, GitHub Copilot app modernization for .NET follows the generated plan and progress tracker to:

- Manage project dependencies
- Apply configuration changes
- Modify application code
- Build the project or solution
- Resolve build and configuration errors
- Detect and fix dependency vulnerabilities
- Check for functional consistency
- Look for migration items missed during the first pass
- Generate a final migration summary

GitHub Copilot may ask for approval before running tools, commands, or Model Context Protocol (MCP) knowledge base operations. Approve the relevant requests during the demo so the migration can continue.

## Demo Tips

- Start from a clean branch so the generated migration changes are easy to review.
- Keep the assessment report visible while explaining the modernization findings.
- Review `plan.md` before continuing so attendees can see how Copilot structures the work.
- Review `progress.md` during the migration to show task tracking.
- Use **Continue** whenever Copilot pauses for confirmation.
- In Visual Studio, the project may reload after configuration updates. If the Copilot Chat window loses focus, return to the chat tab to continue.
- If a modernization session pauses unexpectedly, send `Continue` in chat to resume.

## Suggested Demo Script

1. Introduce Contoso University as a .NET Framework 4.8 application with local infrastructure dependencies.
2. Run the modernization assessment.
3. Highlight findings for file storage, database access, messaging, or secrets.
4. Start one migration task, such as local file system to Azure Blob Storage.
5. Review the generated migration plan and progress tracker.
6. Continue and approve tool usage as Copilot updates the application.
7. Show the validation loop, including build and vulnerability checks.
8. Review the final changed files and migration summary.

## Additional Project Notes

- Teaching material uploads are stored under `Uploads/TeachingMaterials/` before modernization.
- Notification behavior is implemented through the notification model, service, controller, scripts, and styles in this repository.
- The project file is `ContosoUniversity.csproj` and the solution file is `ContosoUniversity.sln`.
