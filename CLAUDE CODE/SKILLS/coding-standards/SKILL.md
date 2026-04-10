---
name: coding-standards
description: "Universal coding standards and quality practices. Technology-agnostic. Preloaded into implementers to ensure baseline code quality regardless of domain. Project-specific conventions come from CLAUDE.md files, not this skill."
user-invocable: false
---

# Universal coding standards

These are technology-agnostic quality standards. They apply regardless of language, framework, or domain.
Project-specific conventions (React patterns, API design, database conventions, etc.) belong in your project's CLAUDE.md files — not here.

## Code structure

- Functions do one thing. If a function needs an "and" in its description, split it.
- Keep functions under ~40 lines. Extract helpers when complexity grows.
- Name things for what they represent, not how they're implemented. `getUserOrders` not `queryDatabaseForOrdersByUserId`.
- Prefer early returns over deep nesting. Guard clauses at the top, happy path at the bottom.
- Group related code together. A reader shouldn't jump between distant sections to understand a single flow.

## Error handling

- Handle errors at the boundary where you can do something meaningful about them. Don't catch-and-rethrow without adding context.
- Distinguish between expected failures (user input validation, missing resources) and unexpected failures (null references, network errors). Handle them differently.
- Error messages should help the next developer. Include what happened, what was expected, and what context is relevant.
- Never swallow errors silently. At minimum, log them.
- Validate inputs at system boundaries (API endpoints, form handlers, external data intake). Trust data inside the boundary after validation.

## Testing

- Test behavior, not implementation. Tests should describe what the code does, not how it does it internally.
- Each test verifies one thing. The test name should read as a specification: "returns empty list when no appointments exist."
- Tests should be independent — running one test must not affect another.
- Prefer real assertions over snapshot tests for logic. Snapshots are for rendering stability, not business rules.
- Test edge cases explicitly: empty inputs, boundary values, error paths, concurrent access.

## Naming

- Booleans read as questions: `isValid`, `hasPermission`, `canEdit` — not `valid`, `permission`, `edit`.
- Collections are plural: `users`, `appointments`, `errors` — not `userList`, `appointmentArray`.
- Functions that return values describe what they return. Functions that perform actions describe the action.
- Constants describe their purpose: `MAX_RETRY_ATTEMPTS` — not `THREE`.
- Avoid abbreviations unless they're universally understood in the domain (`id`, `url`, `html` are fine; `appt`, `mgr`, `btn` are not).

## File organization

- One concept per file. A file named `appointment.js` shouldn't also define calendar utilities.
- File names match what they export. If a file exports `AppointmentStore`, the file is `appointment-store`.
- Keep related files close. Tests next to source (or in a mirrored test directory). Types next to the code that uses them.
- Index/barrel files are for public APIs only. Don't re-export internal implementation details.

## Dependencies and coupling

- Depend on abstractions, not concretions. Pass dependencies in rather than importing singletons.
- Modules communicate through defined interfaces, not by reaching into each other's internals.
- If changing module A forces you to change module B, they're coupled — make the coupling explicit through an interface or extract the shared concern.
- Keep third-party dependencies behind wrappers at the boundary. Don't scatter library-specific calls throughout business logic.

## Comments and documentation

- Code should be self-documenting for the "what." Comments explain the "why."
- Comment non-obvious business rules, workarounds, and architectural decisions.
- Don't comment obvious code. `// increment counter` above `counter++` is noise.
- TODO comments include who and when: `// TODO(dennys, 2025-03): remove after migration completes`

## Security basics

- Never trust user input. Sanitize, validate, escape as appropriate for the output context.
- Don't store secrets in code. Use environment variables or secret management.
- Prefer principle of least privilege — grant minimum access needed.
- Log security-relevant events (auth failures, permission denials) but never log sensitive data (passwords, tokens, PII).
