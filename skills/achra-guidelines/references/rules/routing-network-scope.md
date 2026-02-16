---
title: Network-scoped routes under network/[slug]
category: routing
tags: routing, network, app router
---

## Network-scoped routes under network/[slug]

Routes that depend on a single network (builders, finances, workstreams, roadmaps for that network) live under `app/network/[slug]/...`. Global routes (networks list, services, workstreams list) live under `app/(achra)/...`.

**Incorrect:** Putting a network-specific page at the root or under `(achra)`.

```
app/(achra)/network-builders/[slug]/page.tsx  # Wrong
```

**Correct:**

```
app/network/[slug]/builders/page.tsx
app/network/[slug]/finances/page.tsx
app/(achra)/networks/page.tsx
```

Add `loading.tsx` next to `page.tsx` when the page fetches data.
