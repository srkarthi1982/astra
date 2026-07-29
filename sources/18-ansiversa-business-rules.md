# Ansiversa Business Rules

This file summarizes cross-app rules that should not be guessed. It does not replace each app's `story.md` or `destination.md`.

## Platform

- One account spans the ecosystem.
- The shell owns authentication, routing infrastructure, global navigation, global search, user context, user profile, layout, and theme.
- Mini apps own domain pages, app-specific Zustand stores, app API calls, and app-specific components.
- Mini apps must not own global login, global layout, or parent navigation.
- Overview Explore CTAs must enter the first real workflow route.

## Bill Splitter

- Monetary rounding must preserve bill totals.
- Equal-split remainder distribution must be deterministic.
- Custom allocations must equal the item total before save.
- Participants and items are long-lived bill records and should support visible edit/delete where product rules allow.

## Savings Goal Planner

- Goal progress is based on saved contributions and target amount.
- User-created goals and contributions are owner-scoped.
- Long-lived goal records should support create, edit, and delete.

## Salary Breakdown Calculator

- Salary calculations should keep create/update payloads aligned with backend schemas.
- Saved scenarios are user-owned long-lived records.
- Tax/allowance assumptions must be explicit in UI or docs and not silently inferred.

## Work Log Tracker

- Work logs are user-owned records.
- Time and duration calculations must preserve chronological consistency.
- Historical work entries may be editable when treated as user-authored records.

## Net Worth Tracker

- Currency totals are separated; the app does not silently convert currencies.
- Assets and liabilities determine net worth by currency.
- Included/excluded account behavior affects net worth totals and snapshots.
- Snapshots are immutable historical captures.
- Account names are unique per owner case-insensitively.
- Archived accounts are restore-only for account metadata and do not expose balance edit/delete controls.

## Leave Planner

- Weekend handling, half-day overlap rules, balance calculation, and leave type behavior require app-specific review before changes.

## General Finance Apps

- Never mix currencies without an explicit conversion model.
- Store only frontend-required fields in list/dashboard responses.
- Use Decimal-safe backend calculations for money-like values.

## Astra Read Execution

- Astra may not read app data directly through SQL or app database sessions.
- A governed read requires certified read authorization plus an exact
  app-owned grant.
- The first authorized adapter is Subscription Manager only.
- Read execution is read-only; write and mutation operations remain prohibited.
- Additional app adapters, ASTRA-APP-VAL-001, ASTRA-CHAT-001, provider/model
  integration, and production read execution require separate authorization.
