# Package Ecosystem Patterns

## Dependency File Detection

| Ecosystem | Files | Version Syntax |
|-----------|-------|---------------|
| Node/npm | `package.json`, `package-lock.json` | `"^1.2.3"`, `"~1.2.3"`, `"1.2.3"` |
| Python/pip | `requirements.txt`, `pyproject.toml`, `setup.py`, `setup.cfg`, `Pipfile` | `==1.2.3`, `>=1.2.3`, `~=1.2.3` |
| Python/uv | `pyproject.toml`, `uv.lock` | Same as pip |
| Python/poetry | `pyproject.toml`, `poetry.lock` | `^1.2.3`, `~1.2.3`, `1.2.3` |
| Rust/cargo | `Cargo.toml`, `Cargo.lock` | `"1.2.3"`, `"^1.2.3"`, `"~1.2.3"` |
| Go | `go.mod`, `go.sum` | `v1.2.3` |
| Ruby | `Gemfile`, `Gemfile.lock`, `*.gemspec` | `"~> 1.2"`, `">= 1.2.3"` |
| Java/Maven | `pom.xml` | `<version>1.2.3</version>` |
| Java/Gradle | `build.gradle`, `build.gradle.kts` | `implementation("group:artifact:1.2.3")` |
| .NET | `*.csproj`, `packages.config`, `Directory.Packages.props` | `Version="1.2.3"` |
| PHP/Composer | `composer.json`, `composer.lock` | `"^1.2.3"`, `"~1.2.3"` |
| Swift | `Package.swift` | `.upToNextMajor(from: "1.2.3")` |
| Elixir | `mix.exs` | `"~> 1.2"` |

## Context7 Library Name Mapping

When resolving libraries via context7, use these naming conventions:

- **npm packages**: Use the package name directly (e.g., `react`, `express`, `@angular/core`)
- **PyPI packages**: Use the PyPI name (e.g., `django`, `flask`, `sqlalchemy`)
- **Crates**: Use the crate name (e.g., `tokio`, `serde`, `actix-web`)
- **Go modules**: Use the module path (e.g., `gin-gonic/gin`, `gorilla/mux`)
- **Ruby gems**: Use the gem name (e.g., `rails`, `sinatra`)

## Common Version Verification Queries

Use these query patterns with `query-docs` to find version info:

- `"latest version installation getting started"`
- `"changelog release notes what's new"`
- `"migration guide upgrade breaking changes"`
- `"installation setup quickstart"`
