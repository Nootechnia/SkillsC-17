# Skills Repository

Generic skill templates for C++ projects. This repository contains a complete, reusable set of work guides (skills) that any AI or developer can adapt to new C++ projects — without project-specific code or architecture references.

## What's Inside

The `Skills/` directory includes 17 template files covering the full workflow for C++ project development:

| Skill | Purpose |
|-------|---------|
| `arq.md` | Architecture conventions — modules, design patterns, naming, documentation |
| `code.md` | Code style — indentation, braces, line length, comment sanitizer (no emojis) |
| `fix.md` | Bug correction procedure — identification, analysis, fix development, validation |
| `git.md` | Git workflow — branches, pull requests, team collaboration rules |
| `issues.md` | Issue tracking — types, labels, resolution flow |
| `license.md` | License structure — main license, third-party notices, `.local/` layout |
| `log.md` | Log system — .txt files for long builds, UTC timestamps, append-only policy |
| `memory.md` | Agent work memory — `.local/.agentes/` structure, task plans, branch states |
| `readme.md` | README.md template generator with placeholders (not project-specific) |
| `refactor.md` | Code refactoring — analysis, checklist, validation, risk management |
| `repo.md` | Essential commands — CMake build, tests, platform-independent workflow |
| `test.md` | Test structure — unit/integration/headless, CMake registration, execution |
| `ci.md` | CI/CD configuration — GitHub Actions, GitLab CI examples, test targets |
| `doc.md` | Documentation guide — folder structure, Mermaid/UMI diagrams, formats |
| `feat.md` | New feature guide — proposal, implementation checklist, acceptance criteria |
| `build.md` | Build commands — CMake configs, build types, daily vs CI workflows |

## Key Features

- **Fully generic**: Zero references to FunshiEngineGL/Kromax in the core templates. All placeholders use `< >` format for project-specific values.
- **Consistent structure**: Every skill follows the pattern `## Propósito` → structure → placeholders → integrations.
- **`memory.md` special**: Complete syntax for `.local/.agentes/` with task organization (`plan.md`, `progress.md` append-only) and branch states (`estado-branch.md`).
- **Integrated system**: All skills reference each other appropriately — you're not learning 17 independent documents.
- **No ARQUITECTURA.md**: `arq.md` eliminated all references; it's now a pure template telling you to *create* your own architecture doc.

## How It Works

1. **Start**: Copy `Skills/` to a new repository
2. **Memory**: Use `memory.md` in `.local/.agentes/PLAN-*/`
3. **Plan**: Follow `plan.md` structure, append to `progress.md`
4. **Architecture**: Review `arq.md` for constraints
5. **Code**: Apply `code.md` conventions (comment sanitizer, no emojis)
6. **Build/Tests**: `build.md` / `test.md` conventions
7. **CI**: Configure with `ci.md`
8. **Logs**: Generate in `logs/` following `log.md`
9. **Issues**: Handle with `issues.md`
10. **Commit**: `repo.md` / `git.md` conventions
11. **Finish**: `commit: descripción`, clean or archive `.agentes/`

## Who Is This For

- AI assistants working on C++ projects
- Developers starting a new C++ repo who need structure without opinionated imposition
- Teams wanting a consistent, reusable framework for project-internal guides

## No Hidden Agenda

This is exactly what the description says: 17 template files, a consistent pattern, and nothing tied to a specific engine or framework. Use what you need, discard the rest. No magic, no "best practices" that don't apply to your context, and no requirement to adopt the whole system at once.

---

**Created**: 2026  
**License**: See `Skills/license.md` for guidance on applying licenses to your project.
