---
title: Shared vs domain module placement
category: arch
tags: shared, domain, placement
---

## Shared vs domain module placement

Use the placement decision tree: (1) Used in multiple modules or app root? → `modules/shared/`. (2) Specific to one domain? → `modules/{domain}/`.

**Incorrect:** Putting a shared button in a domain module, or a domain-specific form in shared.

```typescript
// In modules/transaction/components/shared-button.tsx — wrong; shared UI belongs in shared
```

**Correct:**

- Generic UI, feature flags, fetcher, nav config → `modules/shared/`
- Transaction list, transaction form, transaction service → `modules/transaction/`

Reference: [architecture.md](../architecture.md)
