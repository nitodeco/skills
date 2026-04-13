---
name: onboard
description: Onboards a developer into an unfamiliar codebase by producing a structured summary of architecture, tech stack, conventions, and development workflow, then transitions into interactive Q&A. Use this skill when the user is new to a project, asks to be onboarded, wants a codebase overview, says things like "explain this project", "walk me through this repo", "I'm new here", "help me understand this codebase", or wants to understand how a codebase is organized before contributing.
---

# Onboard (codebase orientation)

## When to use

Apply this skill whenever a developer wants to get up to speed on a codebase they are unfamiliar with. This includes joining a new team, picking up an open-source project, reviewing a repo before contributing, or simply trying to understand how things fit together.

## Phase 1: Explore the codebase

Gather information before producing any output. The goal is to build an accurate mental model of the project so the summary is specific and actionable rather than generic. Read broadly first, then go deeper in areas that matter.

### Project identity

1. Read the top-level README, CONTRIBUTING.md, and any docs/ directory if present. These are the maintainers' own description of the project — treat them as ground truth for intent and terminology.
2. Identify the project's **purpose** in one sentence: what problem does it solve, and for whom?

### Tech stack and dependencies

1. Look for package manifests (package.json, Cargo.toml, go.mod, pyproject.toml, requirements.txt, Gemfile, pom.xml, build.gradle, etc.). Identify the language(s), framework(s), and key dependencies.
2. Note the runtime and build tooling: bundlers, compilers, task runners, linters, formatters, test frameworks.

### Folder structure and architecture

1. List the top-level directories and identify what each one contains. Go one level deeper for the main source directory.
2. Identify **entry points**: where does execution start? (e.g., main.ts, index.js, cmd/main.go, app.py). For web apps, identify the routing layer.
3. Look for architectural patterns: monorepo vs single package, MVC, hexagonal, microservices, module boundaries, shared libraries.

### Conventions and patterns

This is important because conventions are the hardest thing for a newcomer to pick up from reading code alone — they are implicit knowledge that the team takes for granted.

1. Look at a few representative source files to identify reused patterns: naming conventions, error handling style, logging approach, how configuration is managed, how tests are structured alongside source code.
2. Check for linter/formatter config (.eslintrc, .prettierrc, rustfmt.toml, .editorconfig, etc.) — these encode the team's style preferences.
3. Look for shared abstractions that appear across the codebase: base classes, utility modules, custom hooks, middleware patterns, decorators, or macros that a newcomer would encounter repeatedly.

### Development workflow

1. Read CI/CD config (.github/workflows/, .gitlab-ci.yml, Jenkinsfile, etc.) to understand how code gets built, tested, and deployed.
2. Check for a Makefile, Justfile, Taskfile, or scripts/ directory — these often reveal the commands developers use day to day.
3. Look for Docker/container config (Dockerfile, docker-compose.yml) if present.
4. Check for environment setup instructions (.env.example, .tool-versions, .nvmrc, .python-version).

### External signals

1. Check recent git history (`git log --oneline -20`) to understand what areas are actively changing.
2. If GitHub CLI is available, check open issues and PRs (`gh issue list --limit 5`, `gh pr list --limit 5`) to get a sense of current work and priorities.
3. Look for a CHANGELOG or release tags to understand the project's maturity and release cadence.

## Phase 2: Present the summary

Produce a structured summary using the sections below. Adapt depth to the project — skip sections that do not apply, expand sections where the project has notable complexity.

### Summary structure

Use actual file paths, module names, and commands from the project — not generic placeholders. The developer should be able to act on every line.

1. **What this project does** — One to three sentences. What problem it solves, who it is for.
2. **Tech stack** — Languages, frameworks, key libraries, build and test tooling.
3. **Architecture overview** — How the code is organized. Major modules and how they relate. Entry points. Data flow at a high level.
4. **Key conventions and patterns** — The reusable patterns a developer will encounter throughout the codebase. Naming conventions, error handling, configuration approach, test structure, shared abstractions.
5. **Development workflow** — How to install dependencies, run the project locally, run tests, and deploy. What CI does.
6. **Active areas** — What is currently being worked on, based on recent git history and open PRs/issues.

Keep the summary concise but specific. Aim for a document a developer can read in a few minutes and walk away with a working understanding of the project.

## Phase 3: Interactive Q&A

After presenting the summary, invite the developer to ask follow-up questions. They know best what they need to understand more deeply — let them steer.

When answering questions:

- **Read the relevant source code before answering.** Do not guess from the summary alone. The summary is a map; the code is the territory.
- **Point to specific files and line numbers** so the developer can follow along in their editor.
- **Explore on demand.** If the developer asks about a part of the codebase not covered in the summary, investigate it before answering rather than speculating.
- **Be honest about boundaries.** If a question is about a third-party library's internals or external infrastructure not visible in the repo, say so and suggest where to look.
