---
title: One component per file
category: conv
tags: component, file, structure
---

## One component per file

Each component file (`*.tsx`) must contain exactly one component (the one that matches the file name). Additional components used only by that component belong in separate files in the same directory (subcomponents). Do not define multiple unrelated components in a single file.

**Incorrect:**

```typescript
// user-card.tsx — multiple components in one file
function UserCard() { ... }
function UserAvatar() { ... }
function UserName() { ... }
export { UserCard }
```

**Correct:**

One component per file: `user-card.tsx`, `user-avatar.tsx`, `user-name.tsx` in the same directory; re-export only what is used elsewhere.

Reference: [conventions.md](../conventions.md)
