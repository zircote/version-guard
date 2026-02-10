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
  This skill prevents security vulnerabilities from outdated versions, wasted migration effort,
  and poor developer experience from deprecated APIs or patterns.
---

# Version Guard

Verify every library version recommendation against live documentation before suggesting it.
Never rely on training-data version knowledge — always check.

## Workflow

### 1. Detect Version-Sensitive Context

Trigger when any of these occur:
- About to recommend a specific package version
- Writing an install command (`npm install`, `pip install`, `cargo add`, `go get`, etc.)
- Adding or modifying dependency files
- Writing code that imports version-sensitive APIs
- User asks about versions, compatibility, or "latest"

### 2. Load Context7 Tools

The context7 tools are deferred and must be loaded before use:

```
ToolSearch query: "+context7"
```

This loads both `mcp__context7__resolve-library-id` and `mcp__context7__query-docs`.

### 3. Resolve the Library

Use the context7 MCP tool to find the library:

```
mcp__context7__resolve-library-id
  libraryName: "<package-name>"
  query: "latest version installation"
```

Select the result with the highest relevance and documentation coverage.

### 4. Query Current Documentation

Retrieve version and installation info:

```
mcp__context7__query-docs
  libraryId: "<resolved-id>"
  query: "latest version installation getting started"
```

Extract:
- Current stable version number
- Installation instructions
- Any noted breaking changes from prior major versions

### 5. Apply the Verified Version

- Use the verified latest stable version in all recommendations and install commands
- If the verified version differs from what training data suggests, note this explicitly:
  `"Using <library> v<latest> (verified current — training data may reference v<old>)"`
- If context7 cannot resolve the library, fall back to checking the package registry directly
  via web search or the project's official documentation, and note the source

### 6. Flag Breaking Changes

When upgrading from a commonly-used older version:
- Note major API changes briefly
- Reference migration docs if available from the context7 query
- Warn about deprecated patterns that training data may still suggest

## Fallback Strategy

If context7 cannot resolve the library:
1. Search the web for `"<library> latest version <current-year>"` to find the official release
2. Check the project's GitHub releases page or package registry (npm, PyPI, crates.io, etc.)
3. Clearly state the source of the version info: `"Per <source>, latest stable is v<X>"`

## Ecosystem Reference

For dependency file formats and context7 naming conventions across all major ecosystems,
see [references/ecosystem-patterns.md](references/ecosystem-patterns.md).
