---
title : "React Frontend"
date : "2026-07-06"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

#### Stack

- **Vite + React + TypeScript**, styled with **Tailwind CSS v4**
- Cognito called directly via its REST API (`InitiateAuth`, `SignUp`, `ConfirmSignUp`) using fetch — no Amplify library needed
- Configuration (API URL, Client ID) extracted to `.env` (not committed), with an `.env.example` for new members
- Team workflow: **branch-per-module + PR**: `feat/api-module`, `feat/auth-ui`, `feat/jobs-ui`...

#### Screens

**Sign in / Sign up / Email confirmation** — self-registration via Cognito with a 6-digit code:

![Login screen](/images/capstone/ui-login.png)

**Job management** — list with color-coded status badges, status filter (mapped to the `?status=` query), create/edit form, delete confirmation modal, CV upload/download:

![Jobs screen](/images/capstone/ui-jobs.png)

#### Token handling

- IdToken + RefreshToken stored in localStorage; the app **auto-refreshes** via `REFRESH_TOKEN_AUTH` when the token has less than 2 minutes left → long demos never lose the session
- All API calls go through a single `call<T>()` helper that attaches the Bearer token

#### Data isolation

Signing in with 2 accounts in 2 browsers: each user only sees their own jobs — confirming the `userId`-based partitioning from the JWT works correctly.
