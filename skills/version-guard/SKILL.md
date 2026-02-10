---
name: version-guard
description: >
  Verify and enforce use of the latest stable library/package versions using live documentation
  lookups instead of training-data knowledge. Use PROACTIVELY whenever:
  (1) Recommending or selecting a library, framework, or package version,
  (2) Adding dependencies to any project (package.json, pyproject.toml, requirements.txt,
  Cargo.toml, go.mod, Gemfile, pom.xml, build.gradle, composer.json, etc.),
  (3) A user asks "what version of X should I use?" or similar version questions,
  (4) Writing code examples that import or configure version-sensitive libraries,
  (5) Suggesting install commands (npm install, pip install, cargo add, go get, etc.),
  (6) Upgrading or auditing existing dependencies.
---

# Version Guard — Proactive Version Verification

You are a version-aware assistant. Before recommending any library version, you MUST verify
the current stable release against live documentation. Never trust training-data version knowledge.

## When to Activate

Trigger automatically when you detect any of these contexts:

- About to recommend a specific package version
- Writing an install command (`npm install`, `pip install`, `cargo add`, `go get`, etc.)
- Adding or modifying dependency files
- Writing code that imports version-sensitive APIs
- User asks about versions, compatibility, or "latest"
- Generating project scaffolds or starter templates

## Verification Workflow

### Step 1 — Load Context7 Tools

The context7 MCP tools are deferred. Load them first:

```
ToolSearch query: "+context7"
```

This loads `mcp__context7__resolve-library-id` and `mcp__context7__query-docs`.

### Step 2 — Resolve the Library

```
mcp__context7__resolve-library-id
  libraryName: "<package-name>"
  query: "latest version installation"
```

Select the result with the highest relevance and documentation coverage.

### Step 3 — Query Current Documentation

```
mcp__context7__query-docs
  libraryId: "<resolved-id>"
  query: "latest version installation getting started"
```

Extract:
- Current stable version number
- Installation instructions
- Breaking changes from prior major versions

### Step 4 — Apply the Verified Version

- Use the verified latest stable version in all recommendations and install commands
- If the verified version differs from training data, note explicitly:
  `"Using <library> v<latest> (verified current — training data may reference v<old>)"`

### Step 5 — Flag Breaking Changes

When upgrading from an older version:
- Note major API changes briefly
- Reference migration docs if available
- Warn about deprecated patterns

## Fallback Strategy

If context7 cannot resolve the library:
1. Search the web for `"<library> latest version <current-year>"`
2. Check GitHub releases or the package registry (npm, PyPI, crates.io, etc.)
3. State the source: `"Per <source>, latest stable is v<X>"`

## Ecosystem Reference

For dependency file formats and context7 naming conventions across all major ecosystems,
see [../../references/ecosystem-patterns.md](../../references/ecosystem-patterns.md).
