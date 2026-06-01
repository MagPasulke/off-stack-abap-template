# off-stack ABAP template

A GitHub template repository for developing ABAP projects outside of a SAP system. Write ABAP in your local IDE, lint it, run unit tests locally via transpilation, and sync to a real SAP system when ready.

[Create a repository from this template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template)

## what's in it?

### abaplint

Static analysis for ABAP running locally and in CI. Catches syntax errors, naming conventions, and common issues without a SAP system.  
[abaplint documentation](https://abaplint.org/)

### abap transpiler

Transpiles ABAP to JavaScript so you can run ABAP Unit tests locally with `npm run unit` — no SAP system required.  
[open-abap documentation](https://open-abap.org/)

### GitHub workflows

#### ci

Runs `npm test` (lint + transpiled unit tests) on every push and pull request.

#### release-please

Automates versioning and changelog generation from [conventional commits](https://www.conventionalcommits.org/). Creates release PRs automatically when changes land on `main`.  
[release-please documentation](https://github.com/googleapis/release-please)

### AI agent skills & agents.md

The `.agents/skills/` folder contains skills that teach AI coding agents how to create ABAP repository objects in the correct [abapGit file format](https://docs.abapgit.org/user-guide/reference/folders-filenames.html#files). Skills are available for:

- **abapGit object creation** — CLAS, INTF, TABL, DDLS, DTEL, DOMA, BDEF, SRVD, SRVB, FUGR, and more
- **ADT remote operations** — trigger abapGit pull and run ABAP Unit tests on a connected SAP system
- **conventional-commit** — guides standardized commit messages

These skills work with any IDE or AI agent that supports the skills concept.  
[agents.md specification](https://agents.md/)

### scripts & opencode tools

TypeScript scripts in `scripts/` and `.opencode/tools/` for interacting with a remote SAP system via ADT (ABAP Development Tools). These are optional and require `.env` configuration (see below).

> **Note:** This template currently includes an opinionated setup for [opencode](https://opencode.ai/) usage. In the future, additional options may be added to support other tools that can leverage the same scripts.

## getting started

### prerequisites

- [Node.js](https://nodejs.org/) 
- [VS Code](https://code.visualstudio.com/) with the [Standalone ABAP Development](https://marketplace.visualstudio.com/items?itemName=larshp.standalone-abap-development) extension. Any other IDE also works, but less convenient.
- SAP system with [abapGit](https://docs.abapgit.org/) installed (needed to deploy and run on a real system)

### copy this template

Click **"Use this template"** on GitHub to create your own repository.

### install dependencies

```bash
npm install
```

### create abapGit repo & root package

Create a package on your SAP system and link it to your new GitHub repository via abapGit.  
[abapGit: linking a repository](https://docs.abapgit.org/user-guide/projects/online/install.html)

### sync remote with root package

Push the root package from SAP once via abapGit so it appears in your repository. Then pull the repo locally in VS Code and start developing.

### optional: configure abaplint

Edit `abaplint.json` to adjust rules, naming conventions, and target ABAP version for your project. The repository currently includes a reduced starting configuration.
[abaplint rules reference](https://rules.abaplint.org/)

### optional: maintain GH secrets for release-please

Create a GitHub Personal Access Token (PAT) and add it as a repository secret named `MY_RELEASE_PLEASE_TOKEN`.  
[release-please setup](https://github.com/googleapis/release-please?tab=readme-ov-file#setting-up-release-please)

### optional: maintain .env for SAP system connection

Copy `.env.example` to `.env` and fill in your SAP ADT connection details. This enables the ADT scripts for remote abapGit pull and unit test execution. These scripts can be used to sync your sap dev system without leaving the IDE. Or to be included in a pipeline.

```
SAP_ADT_URL=https://your-sap-system:port
SAP_ADT_USER=DEVELOPER
SAP_ADT_PASSWORD=your-password-here
SAP_ROOT_PACKAGE=$YOUR_ROOT_PACKAGE_NAME
```

### optional: maintain AGENTS.md

Edit `AGENTS.md` to describe your project. AI agents use this file to understand your codebase context.  
[agents.md specification](https://agents.md/)



