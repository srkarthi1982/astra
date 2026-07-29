# Ansiversa Shared Resources

## Frontend Components

| Resource | Purpose | Import Path | Usage Contract | Restrictions |
| --- | --- | --- | --- | --- |
| AvFormDrawer | Shared drawer form for create/edit workflows. | `@shared/components/forms` or `@shared/components/forms/AvFormDrawer` | Use for established mini-app create/edit drawers with prefilled edit values. | Do not send create-only parent IDs in update payloads unless backend update schema supports reassignment. |
| AvRecordActions | Icon-style edit/delete actions for saved records. | `@shared/components/AvRecordActions` | Use for existing record actions where practical; provide accessible labels. | Do not expose edit controls for generated output or read-only archived records. |
| AvConfirmDialog / useAvConfirmDialog | Shared confirmation dialog pattern. | `@shared/components/AvConfirmDialog`, `@shared/components/useAvConfirmDialog` | Use for destructive or irreversible actions. | Confirmation copy must match the action. |
| AvPagination | Standard pagination control. | `@shared/components/AvPagination` | Use for list screens with page/pageSize data. | Do not invent separate pagination UI without approval. |
| AvAuthenticatedPageState | Authenticated workflow gate. | `@shared/components/AvAuthenticatedPageState` | Wrap protected mini-app workflow pages. | Mini apps must not own authentication architecture. |
| AvAppOverviewPage | Standard overview page renderer. | `@shared/components/AvAppOverviewPage` | Use for app overview metadata and Explore CTAs. | Explore must route into the first real workflow, not back to overview. |
| AvInlineFeedback | Inline single-message state. | `@shared/components/AvInlineFeedback` | Use for compact success/error/warning feedback. | Do not replace with inconsistent ad hoc banners. |
| AvFeedbackStack | Shared stacked feedback state. | `@shared/components/AvFeedbackStack` | Use when pages need both error and success feedback. | Keep feedback actionable and concise. |
| AvCardEmptyState | Card-scoped empty-state content. | `@shared/components/AvCardEmptyState` | Use inside repeated-card/list areas. | Avoid using cards inside cards. |
| AvBusyIndicator | Shared busy indicator. | `@shared/components/AvBusyIndicator` | Use for consistent loading affordances. | Avoid page-level spinner loops when loaders/stores can provide ready data. |

## Shared Stores And Helpers

| Resource | Purpose | Import Path | Usage Contract |
| --- | --- | --- | --- |
| withStoreBusy | Wrap async store actions with busy state. | `@shared/stores/storeHelpers` | Use in Zustand stores for predictable loading behavior. |
| throwApiResponseError | Normalize API failure handling. | `@shared/stores/storeHelpers` | Use before consuming response data. |
| requireStoreData | Assert required response payloads. | `@shared/stores/storeHelpers` | Use to avoid silently rendering missing data. |
| getStoreErrorMessage | Convert unknown exceptions into user-safe store errors. | `@shared/stores/storeHelpers` | Keep messages user-safe and non-secret. |
| useBusyStore | Shared busy state store. | `@shared/stores/useBusyStore` | Use only for shared/global busy behavior. |
| useContentStore | Content metadata state. | `@shared/stores/useContentStore` | Keep content metadata outside mini-app domain stores. |
| useOverviewStore | Overview metadata state. | `@shared/stores/useOverviewStore` | Use for app overview metadata retrieval. |

## Shared Services

| Resource | Purpose | Import Path | Usage Contract |
| --- | --- | --- | --- |
| API client | Generated OpenAPI client wrapper. | `@shared/api/client` | Use generated routes and schemas instead of hand-rolled fetch calls. |
| Generated schema | Type source for API DTOs. | `@shared/api/generated/schema` | Keep regenerated after backend API changes. |
| Apps service | Parent app catalog API access. | `@shared/api/services/apps.service` | Use for platform-level app metadata. |
| Auth service | Authentication API access. | `@shared/api/services/auth.service` | Shell owns auth; mini apps consume auth state. |
| Content/Overview services | App overview metadata. | `@shared/services/content.service`, `@shared/services/overview.service` | Use for overview pages and catalog-driven content. |

## Routing And Shell

The persistent shell owns routing infrastructure, navigation, global search, user context, profile, layout, and theme. Mini apps export route modules under `src/modules/<slug>/index.tsx` and should not replace shell routing.

## Apps Using These Resources

These shared resources are broadly used across the mini-app modules under `ansiversa/src/modules`. For exact current usage, search imports for the resource name before changing a shared API.
