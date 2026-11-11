---
name: project-development
description: >-
  Applies project development standards for UI, security, code quality, wording,
  planning, architecture, data integrity, testing, performance, deployment,
  scope, and documentation. Use when the user calls /project-development or asks
  to follow the project development rules. Works in any project.
disable-model-invocation: true
---

# Project development

Follow this skill for the current task in whatever project is open. Read the project before changing it. If that project has stricter local rules, follow those as well. Do not copy this skill into the project unless the user asks.

For UI, follow `/harrisons-ui` when that skill is available. Before `/publish-new-version`, complete the security audit in this skill and fix vulnerabilities before publishing.

## Workflow

### 1. Understand

Review requirements, existing structure, files, logic, dependencies, and workflows. Note conflicts, risks, and limits. Ask when an essential requirement is unclear.

### 2. Plan

List the files to change and the impact on frontend, backend, database, and API. Check security, data integrity, and performance. Use the simplest reliable approach. Present the plan before a major or high-impact change.

### 3. Build

Follow `/harrisons-ui` for UI. Follow existing architecture and conventions. Make focused, maintainable changes. Protect existing functionality and data. Skip unnecessary dependencies and edits.

### 4. Verify

Check correctness and that the app builds. Test the change, frontend/backend integration, data integrity, and security. Regression-check affected features. Fix issues and retest.

### 5. Complete and report

Never claim completion while important verification is still outstanding. Report:

- **Changes:** what was implemented or modified
- **Files:** important files affected
- **Testing:** what was tested and the results
- **Security:** vulnerabilities found and their status
- **Outstanding:** unresolved issues, limitations, or follow-up

## Standards

### UI and UX

`/harrisons-ui` is the design standard for every UI/UX change. Follow it for layout, components, and visual decisions.

- Aim for professional UX that a first-time user can complete without extra explanation.
- Use responsive layouts, clear navigation, consistent spacing, and consistent components.
- Keep the same visual language across pages.
- Give every element a purpose. Do not add controls, decoration, or copy that do not help the task.
- Account for screen size, device, and interaction (pointer, keyboard, and touch).
- Do not change the design in ways that hurt existing workflows.

### Security

Review security before changing code. Write code that stays secure by default.

- When `/publish-new-version` is called, complete a security audit before the release and fix vulnerabilities before publishing.
- Where they apply, review authentication, authorization, access control, API endpoints, database permissions, and input validation.
- Never expose, share, hardcode, or unnecessarily log credentials, API keys, tokens, passwords, or secrets.
- Never bypass existing security controls.
- Do not leak sensitive information through the frontend, error messages, logs, or API responses.
- A user may access only what they are authorized for.
- Verify a security fix still leaves the feature working.

```text
Bad:  const apiKey = "sk_live_abc123"; console.log(apiKey);
Good: const apiKey = process.env.API_KEY; // never log apiKey or other secrets
```

### Code quality

Write code that is readable, consistent, and simple.

- Follow the existing architecture, naming, and project standards.
- Do not duplicate logic or add dependencies that are not needed.
- Prefer reusable components and functions, each with one focused responsibility.
- Avoid edits that the task does not need.
- Leave the code so a later developer can understand and extend it.
- Handle errors instead of ignoring them.
- Do not introduce breaking changes.
- Remove unused code when it is safe to do so.
- Do not shorten code by giving up reliability or readability.

### Wording

Use simple language in every label, message, and instruction the user sees.

- Say what the control or screen does. Keep terminology the same across the app.
- Write errors that state what happened and what to do next.
- Keep the tone professional and natural.

```text
Bad:  "NullReferenceException at line 42."
Good: "We could not save this. Check the required fields and try again."
```

### Planning

Understand the work before building it.

- Review the requirements, the current structure, the logic, the dependencies, and the workflows.
- See what already exists before creating something new.
- Understand how the feature interacts with the rest of the app.
- Clarify conflicts before choosing a direction.
- Identify limits, risks, and dependencies.
- Do not assume business rules or what the user expects.
- Consider who and what the change affects.
- Present a practical approach before major changes.
- Do not start coding while an essential requirement is still unclear.

### Architecture

Build so the app can grow without extra complexity.

- Follow the existing architecture unless there is a strong reason to change it.
- Keep frontend, backend, database, and business logic separate.
- Reuse what already exists when it fits.
- Keep boundaries between those layers clear.
- Avoid overengineering and extra dependencies.
- Consider later expansion, and do not build features that are not needed now.
- Stay compatible with current behavior.
- Document an important architectural decision when one is necessary.
- Ask before a major architectural change.

### Data integrity

Keep data accurate, consistent, and reliable.

- Validate input before saving it.
- Handle missing, duplicate, invalid, and unexpected data.
- Prevent accidental loss, corruption, and updates the user did not intend.
- Schema or relationship changes must not break existing data.
- Never assume API or database data is already valid.
- Validate on the frontend and again on the backend.
- Display the same data the same way everywhere it appears.
- Use safe operations and transactions where a partial write would be harmful.
- Protect production data when changing structures or records.

```text
Bad:  Save the request body with no check for missing fields, duplicates, or a missing record.
Good: Reject invalid input, then write inside a transaction so a failure does not leave a partial update.
```

### Testing

Verify the work before calling it complete.

- Test every change.
- Cover normal input, edge cases, and unexpected input.
- Check frontend and backend integration.
- Confirm existing behavior still works.
- Regression-check related features.
- Where they apply, test the API, the database, and permissions.
- Fix issues before marking the work done.
- Never claim something works without verifying it.
- Report tests that could not be run.
- Do not hide unresolved issues.

### Performance

Keep load times short, interactions responsive, and processing efficient.

- Avoid extra API calls, extra queries, and repeated work.
- Consider data volume and concurrent users.
- Use pagination, filtering, and optimized queries where they fit the task.
- Do not load data the screen or job does not use.
- Optimize only where it is needed, and do not hurt readability or reliability to do it.
- Do not trade accuracy or security for speed.
- Consider resource use and how usage will grow.

### Deployment

Release only after the change, the config, and the build have been checked.

- Review changes before a commit or a publish.
- Keep development, test, and production separate.
- Never overwrite production data or config unintentionally.
- Keep version history clear and write meaningful change descriptions.
- Plan rollback or recovery for an important release.
- Verify environment variables and deploy config.
- Never commit credentials or secrets.
- The app must build before it is published.
- Run a security audit before `/publish-new-version`.
- Verify the app after deployment.
- Report release status and any outstanding issues.

### Scope

Do only the work that was requested or that the task requires.

- Do not change unrelated features, workflows, or config.
- Do not add a dependency without a valid reason.
- Do not redesign or refactor when the task does not need it.
- Ask before a major change to architecture, the database, or business logic.
- Do not remove a feature without approval.
- Put extra recommendations in a separate note, not in the change itself.
- If a change affects other features, explain that impact before proceeding.

### Documentation

Keep documentation aligned with what the app actually does.

- Update docs when a feature, workflow, API, or config changes.
- Document important setup steps and dependencies.
- Explain complex business logic where a reader cannot see it from the code alone.
- Skip documentation that only repeats the code.
- Write so a later developer can run, maintain, and troubleshoot the app.
- Never write an assumption as if it were a fact.

## Principles

1. Understand before building.
2. Keep the user experience simple and seamless.
3. Security must never be compromised for convenience.
4. Protect existing functionality and data.
5. Prefer simple, reliable, and maintainable solutions.
6. Test before claiming completion.
7. Do not make assumptions about important requirements.
8. Keep communication clear, honest, and straightforward.
9. Make only necessary changes.
10. Prioritize long-term reliability over quick fixes.
