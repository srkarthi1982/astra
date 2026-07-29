# UI Contracts

This file is the frontend source of truth for Ansiversa shell and mini-app UI behavior.

## Platform UI Principle

Ansiversa is one platform. Mini apps must feel like workflows inside the same shell, not separate products with separate UI systems.

## Shell Ownership

The shell owns authentication, routing infrastructure, navigation, global search, user context, profile, layout, and theme. Mini apps render inside the shell and must not replace shell navigation or authentication flows.

## Shared Components

Use established shared components before creating module-local equivalents:

- `AvAppOverviewPage` for overview pages.
- `AvAuthenticatedPageState` for protected workflow gates.
- `AvFormDrawer` for create/edit drawers.
- `AvRecordActions` for saved-record edit/delete actions.
- `useAvConfirmDialog` or `AvConfirmDialog` for destructive confirmations.
- `AvPagination` for paginated lists.
- `AvInlineFeedback` and `AvFeedbackStack` for user feedback.
- `AvPageHeader`, `AvSectionHeader`, `AvCardEmptyState`, `AvBusyIndicator`, and `Card` where existing patterns fit.

Do not introduce a shared abstraction before repetition justifies it. Follow the Rule of 4.

## Overview Contract

Every mini app overview must use canonical metadata and provide an `Explore` CTA. Primary and final CTAs should be labeled `Explore` and route to the first real workflow route. They must not route back to the overview, an empty placeholder, a coming-soon stub, or an unprotected dead end unless Partner/Astra explicitly approve an exception.

## Page Header Contract

Page headings describe the object or workflow. Buttons describe only the action, such as `Create`, `Add`, `Save`, `Update`, `Start`, `Generate`, `Review`, or `Finish`. Avoid labels such as `Create Project` when the page title already gives the object context.

## AvFormDrawer Contract

Use `AvFormDrawer` or the established shared form pattern for long-lived user-created records. Create drawers start with clean defaults. Edit drawers must be prefilled from the selected record or detail endpoint. Save must update the existing record, close the drawer on success, refresh visible data, and show shared feedback.

Do not reuse create payloads blindly for update requests. Parent IDs that are create-only must not be sent during update unless the backend update schema explicitly supports reassignment.

## Drawer Rules

Drawers are for focused create/edit tasks, not full navigation. They should have a clear title, concise fields, a primary submit action, a cancel/close action, validation feedback, and loading state. Avoid nested drawers.

## Delete Confirmation Rules

Destructive actions require confirmation. Confirmation copy must identify the consequence, not just repeat the button label. Delete buttons on saved records should use icon-only actions where practical and must include accessible labels.

## CRUD Consistency

User-created long-lived records should support visible create, read, update, and delete unless the product intent says otherwise. Historical records may be read-only or delete-only. Generated system output should not be editable by default; regeneration is the preferred action when supported.

## Authenticated Page Layout

Protected workflow screens must render through `AvAuthenticatedPageState` or the established protected workflow component for that module. Guest users should see a login-required state rather than broken data fetching.

## Feedback And State

Every workflow needs clear loading, empty, error, and success states. Use shared feedback components. Do not expose raw server errors, stack traces, secrets, or implementation details.

## Pagination And Filtering

Paginated screens should use `AvPagination` and stable page/pageSize semantics. Filters should reset to page 1 when the result set changes. Keep list views lightweight and avoid loading detail-only payload fields.

## Responsive Rules

The platform uses one adaptive codebase. Desktop uses the shell sidebar, tablet uses compact navigation, and mobile uses drawer/bottom navigation patterns. Text must fit inside controls, cards, and panels. Buttons should use compact action labels to avoid wrapping.

## Styling Rules

Prefer shared CSS tokens and Tailwind utility patterns already used by the repo. Do not add unrelated visual systems, heavy gradients, decorative orbs, inline styles, or one-off component libraries without approval.

## Accessibility Baseline

Icon-only controls require `aria-label`, `title`, tooltip text, or an equivalent supported label. Interactive controls must be keyboard reachable and visually identifiable.
