# Architecture

**Version 0.1.0 (draft)**

All components, logic, and related code live under domain-specific modules in the `modules/` directory. This keeps separation of concerns and maintainability.

## Module-based layout

- **Shared**: `modules/shared/` — Used by multiple modules or by the app root (layout, pages).
- **Domain**: `modules/{module-name}/` — Everything specific to one business domain.

Nothing lives in a generic `app/components/`, `components/`, or `src/components/` at the repo root; it all goes under `modules/`.

## Shared module

**Location**: `modules/shared/`

**Typical structure**:

```
modules/shared/
  ├── components/   # Shared UI (app-sidebar, site-header, ui primitives)
  ├── hooks/        # Shared React hooks
  ├── lib/          # Shared utilities (feature-flags, fetcher, utils)
  ├── providers/    # Shared context providers
  ├── types/        # Shared TypeScript types at module root only: use types.ts by default; use types/ folder only when split (e.g. types/transaction.ts, types/something.ts). No types.ts inside lib/, utils/, or other subfolders. No index.ts or types.ts inside types/
  └── config/       # Shared config (e.g. navbar)
```

**When to use**: Put code in `shared` when it is used in more than one domain module or in the app root (layout, global pages). Generic UI (buttons, dialogs, navigation) and cross-cutting concerns (feature flags, fetcher) belong here.

## Domain modules

**Location**: `modules/{module-name}/`

**Typical structure**:

```
modules/{module-name}/
  ├── components/   # Module-specific components
  ├── lib/          # Module-specific utilities
  ├── hooks/        # Module-specific hooks
  ├── providers/    # Module-specific context (if needed)
  ├── types/        # Module-specific types at module root only: use types.ts by default; use types/ folder only when split (e.g. types/transaction.ts, types/something.ts). No types.ts inside lib/, utils/, or other subfolders. No index.ts or types.ts inside types/
  ├── services/     # Domain services (optional)
  ├── graphql/      # GraphQL operations (optional)
  └── mocks/        # Mocks for this domain (optional)
```

**When to use**: Put code in a domain module when it is only used within that domain or is tightly coupled to that domain’s business logic.

**Examples**: `modules/builders/`, `modules/finances/`, `modules/workstream/`, `modules/networks/`, `modules/expense-reports/`.

## Component placement decision tree

1. **Is it used in multiple modules or in the app root?**
   - Yes → `modules/shared/components/` (or shared hooks/lib as appropriate).
   - No → go to step 2.

2. **Is it specific to a single domain?**
   - Yes → `modules/{domain-name}/components/` (or that domain’s hooks/lib).
   - No → Re-evaluate (e.g. split into shared + domain pieces).

## Import patterns

**From shared**:

```typescript
import { Button } from '@/modules/shared/components/ui/button'
import { useMobile } from '@/modules/shared/hooks/use-mobile'
import ff from '@/modules/shared/lib/feature-flags'
```

**From a domain module**:

```typescript
import { TransactionList } from '@/modules/transaction/components/transaction-list'
import { useTransactionForm } from '@/modules/transaction/hooks/use-transaction-form'
```

Use the `@/modules/` alias; do not use relative paths that escape the module (e.g. `../../../shared/`).

## Best practices

1. **Keep modules focused** — One domain or feature area per module.
2. **Minimize cross-module dependencies** — Prefer depending on `shared` rather than domain A depending on domain B.
3. **Shared code goes to shared** — If two or more modules use it, it belongs in `shared`.
4. **Co-locate** — Keep a feature’s components, hooks, and utilities in the same module.
5. **Use index files** — Export module components through `index.ts` for cleaner imports.
6. **Component files are component-only** — Put shared logic and helpers in the module’s `lib/` (or utils); keep component files to a single component and minimal JSX-related logic. See [conventions.md](conventions.md).
7. **Reusable types at module root only** — Put reusable TypeScript types (interfaces, type aliases, enums) in `types.ts` at the root of the module or, when split, in a `types/` folder at module root (e.g. `types/transaction.ts`, `types/something.ts`); no index and no inner types.ts. Do not put types.ts in lib/, utils/, or any other subfolder. Component props must stay in the component file. See [conventions.md](conventions.md).

## Correct vs incorrect structure

**Correct**:

```
modules/
  ├── shared/
  │   ├── components/
  │   │   ├── app-sidebar/
  │   │   │   ├── app-sidebar.tsx
  │   │   │   └── index.ts
  │   │   └── ui/
  │   └── hooks/
  │       └── use-mobile.ts
  └── transaction/
      ├── components/
      │   ├── transaction-list/
      │   │   ├── transaction-list.tsx
      │   │   └── index.ts
      │   └── transaction-form/
      │       ├── transaction-form.tsx
      │       └── index.ts
      ├── hooks/
      │   └── use-transaction-form.ts
      └── lib/
          └── transaction-service.ts
```

**Incorrect**:

```
app/components/transaction-list.tsx   # Should be in modules/transaction/
components/shared/button.tsx           # Should be in modules/shared/
src/components/transaction.tsx        # Should be in modules/transaction/
```
