---
name: e2e
description: Analyze the current project and generate Playwright end-to-end tests automatically.
---

# /e2e — Generate Playwright E2E Tests

Analyze the current project and generate Playwright end-to-end tests automatically.

## When to use
User invokes `/e2e` to generate or regenerate e2e tests for any web or React Native (Expo web) project.

## Steps

1. **Discover the project stack:**
   - Read `package.json` to identify the framework (React, React Native/Expo, Next.js, Vue, etc.)
   - Check for existing test config or `tests/` directory
   - Identify if Playwright is already installed; if not, install it and chromium

2. **Identify screens and routes:**
   - Look for screen/page components (e.g. `src/screens/`, `src/pages/`, `app/`)
   - Look for route definitions (React Router, React Navigation, Next.js file routing, etc.)
   - Look for auth screens (login, register, signup)
   - Look for API service files to understand what the app does

3. **Identify test config:**
   - Look for a `tests/config.json` or prompt the user for:
     - App URL (default: `http://localhost:3000`)
     - Test account credentials (if auth exists)
     - Any screens or flows to skip
   - Save the config to `tests/config.json` for future runs

4. **Generate tests in `tests/` directory:**
   - Create one test file per logical flow (e.g. `tests/auth.ts`, `tests/navigation.ts`, `tests/crud.ts`)
   - Create a `tests/run.ts` entry point that runs all test files and reports results

5. **Test patterns to detect and generate:**

   **Auth (if login/register screens exist):**
   - Login with valid credentials succeeds
   - Login with invalid credentials shows error
   - Registration flow works (if safe to test)
   - Logout returns to auth screen

   **Navigation (if tabs/routes exist):**
   - All navigation tabs/links are visible after login
   - Each tab/route loads without errors
   - Page headings or key elements are present

   **CRUD (if list/form screens exist):**
   - Can open the create/add form
   - Can fill in and submit the form
   - New item appears in the list
   - Can delete an item
   - Clean up test data after each test

   **Forms (if input components exist):**
   - Required field validation works
   - Form submits with valid data
   - Follow-up prompts or modals appear when expected

6. **Test file conventions:**
   - Import from `playwright` (not `@playwright/test` — keep it lightweight)
   - Load config from `tests/config.json`
   - Each test file exports an async function that takes a browser instance
   - Use `page.getByText()`, `page.getByRole()`, `page.locator()` with `.first()` to avoid strict mode issues
   - Use `{ force: true }` on clicks that may be obscured by sticky navbars
   - Use `waitForTimeout` after navigation and form submissions
   - Clean up any created test data at the end of each test
   - Print PASS/FAIL for each assertion with a summary at the end

7. **After generating:**
   - Run the tests to verify they pass
   - Fix any selector issues (strict mode violations, timing, etc.)
   - Report results to the user

## Config file format (`tests/config.json`)
```json
{
  "appUrl": "http://localhost:8082",
  "auth": {
    "email": "test@example.com",
    "password": "password123"
  },
  "skipFlows": []
}
```

## Important
- Never hardcode credentials in test files — always read from config
- Always clean up test data (delete items created during tests)
- Start required servers before running tests if they're not already running
- Don't save screenshots unless the user asks for them
