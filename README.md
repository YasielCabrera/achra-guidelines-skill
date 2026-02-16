# Achra Guidelines Skill

Skills for [Achra.com](https://achra.com). Packaged instructions so AI agents follow Achra platform guidelines, architecture, and conventions when working in the Achra codebase.

Skills follow the [Agent Skills](https://agentskills.io/) format.

## Available Skills

### achra-guidelines

Achra platform guidelines for architecture, conventions, business domains, and technical patterns. Covers module placement, naming, routing, GraphQL, feature flags, skeleton loading, and tech stack.

**Use when:**
- Writing or refactoring Achra code (components, pages, services, hooks)
- Creating skeleton loaders, loading placeholders, or Suspense fallbacks
- Adding modules, features, or routes
- Answering questions about Achra architecture, conventions, or tech stack

**Categories covered:**
- Architecture (shared vs domain modules, placement)
- Conventions (kebab-case, component structure, types)
- Routing (App router, network-scoped routes)
- Data & GraphQL (domain graphql, generated code)
- Feature flags (when and where to use)
- Skeleton loading (layout mirroring, sizing, contrast)
- Tech stack (Next 16, React 19, Tailwind 4, shadcn, GraphQL)

**Commands:** The `commands/` folder contains task specs (e.g. `skeleton.md`) that direct the agent to use achra-guidelines for specific workflows.

## Installation

```bash
npx skills add https://github.com/YasielCabrera/achra-guidelines-skill --skill achra-guidelines
```

Or, if published on [skills.sh](https://skills.sh/):

```bash
npx skills add YasielCabrera/achra-guidelines-skill achra-guidelines
```

Requires Node.js and an agent that supports skills (e.g. Cursor).

## Usage

Reference the skill when working in Achra code. In Cursor: `@achra-guidelines` or `@.cursor/skills/achra-guidelines`.

**Examples:**
```
Create a skeleton component for this <component>
```
```
Add a new module following Achra conventions
```
```
Where should this component live in the Achra codebase?
```

## License

See the repository license file.
