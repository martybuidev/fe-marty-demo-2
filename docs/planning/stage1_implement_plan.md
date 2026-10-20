# Stage 1: Frontend Setup — Implementation Plan

**Stack:** Next.js App Router, TypeScript, Tailwind CSS, Better Auth client,
TanStack Query, and Orval.

**Goal:** Establish the frontend foundation and connect it to the NestJS backend.

## PR #1 — [Chore] Initialize Next.js

- Verify the generated App Router, TypeScript, and Tailwind setup.
- Use `src/app` and configure the `@/*` alias.
- Remove starter page content and unused assets.
- Pin Node.js and pnpm versions.
- Verify local development and production builds.

## PR #2 — [Chore] Configure Development Tooling

- Configure ESLint and Prettier.
- Add lint, typecheck, format, and format-check scripts.
- Add a concise pull request template.
- Document local setup and verification commands.

## PR #3 — [Feat] Configure Environment Validation

- Configure T3 Env with Zod.
- Separate server-only and public client variables.
- Configure the backend API URL and frontend URL.
- Add `.env.example` without credentials.
- Verify missing or invalid required values fail clearly.

## PR #4 — [CI] Setup Tests and GitHub Actions

- Configure Vitest and React Testing Library.
- Add meaningful tests for the configuration introduced so far.
- Run lint, typecheck, format checks, tests, and build in CI.
- Configure CI environment values needed for validation and builds.
- Add component tests alongside features in subsequent PRs.

## PR #5 — [Feat] Implement Shared UI Foundation

- Add only the UI primitives needed initially: buttons, inputs, form fields,
  and toast feedback.
- Add error boundaries, loading states, and a not-found page.
- Keep routing in `src/app` and reusable code in `src/shared`; introduce
  `src/modules` and `src/features` as concrete functionality is added.
- Avoid importing the entire Postline component library upfront.

## PR #6 — [Feat] Setup API and Query Providers

- Configure Axios with credentials for backend session cookies.
- Handle the backend success envelope and error contract consistently.
- Configure TanStack Query and development tools.
- Define retry and error handling without duplicate toast notifications.
- Do not copy NextAuth bearer-token or refresh-token interceptors from Postline.

## PR #7 — [Feat] Integrate Better Auth Client

- Configure the React Better Auth client against the NestJS auth server.
- Support session lookup and logout.
- Verify browser requests receive and send the session cookie correctly.
- Verify allowed origins and adjust CORS only if integration requires it.
- Use the Better Auth client rather than Orval for authentication. Do not set up
  a second auth server in Next.js.

## PR #8 — [Feat] Implement Authentication Pages

- Implement registration and login using the Better Auth client.
- Add form validation, field errors, pending states, and redirect behavior.
- Add component tests and browser checks for supported auth flows.
- Defer forgot/reset password and email verification until the backend supports
  those flows. Google OAuth remains a separate feature.

## PR #9 — [Feat] Implement Protected Application Layout

- Add the authenticated application layout and navigation.
- Display the current user and provide logout.
- Handle unauthenticated access and expired sessions.
- Keep backend authorization authoritative; frontend route checks are for UX.

## PR #10 — [Chore] Integrate Orval

**Prerequisite:** The backend exposes its first business API with a useful
OpenAPI contract. Do not generate an empty client just to complete setup.

- Generate API clients and models from NestJS `/api/docs-json`.
- Split generated output into readable files, separate from handwritten code.
- Connect generated requests to the shared transport and query layer.
- Keep feature logic, cache policy, and UI mapping outside generated files.
- Verify generated types match the backend response envelope and errors.
- Continue using the Better Auth client for authentication.
