# Tern CLI 🩺

<p align="center">
  <strong>Find out why your development environment is broken.</strong><br />
  Diagnose Node.js projects, environment variables, ports, Git, deployments, AI coding agents, and MCP — in one command.
</p>

<p align="center">
  <a href="https://www.npmjs.com/package/tern-cli"><img src="https://img.shields.io/npm/v/tern-cli.svg?style=flat-square&color=blue" alt="npm version" /></a>
  <a href="https://www.npmjs.com/package/tern-cli"><img src="https://img.shields.io/npm/dm/tern-cli.svg?style=flat-square&color=blue" alt="npm downloads" /></a>
  <a href="https://github.com/terngg/tern"><img src="https://img.shields.io/badge/tests-102%20passed-brightgreen.svg?style=flat-square" alt="Tests Status" /></a>
  <a href="https://github.com/terngg/tern/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-MIT-green.svg?style=flat-square" alt="License: MIT" /></a>
  <a href="https://nodejs.org"><img src="https://img.shields.io/badge/node-%3E%3D18.0.0-brightgreen.svg?style=flat-square" alt="Node.js Version" /></a>
  <a href="https://github.com/terngg/tern/stargazers"><img src="https://img.shields.io/github/stars/terngg/tern?style=flat-square&color=yellow" alt="GitHub Stars" /></a>
</p>

<p align="center">
  <img src="assets/tern-demo.svg" alt="Tern CLI Terminal Demo" width="820" />
</p>

---

## ⚡ Try It in 5 Seconds (No Install Needed)

Run directly in any project folder:

```bash
# 1. Diagnose developer environment & common project issues
npx tern-cli doctor

# 2. Diagnose AI coding agents (Codex, Claude Code, Gemini CLI, OpenCode, MCP)
npx tern-cli agent
```

<details>
<summary>📦 Or install globally as a system CLI</summary>

```bash
# Using pnpm
pnpm add -g tern-cli

# Using npm
npm install -g tern-cli

# Using yarn
yarn global add tern-cli
```
</details>

---

## 💡 What is Tern CLI?

**Tern CLI** is an open-source developer doctor that eliminates environment friction for traditional Node.js stacks and modern AI-assisted coding tools:

- 🩺 **Traditional Doctor**: Detects port conflicts (PID inspection & safe kill), missing `.env` variables compared to `.env.example`, uncommitted secrets in Git, broken lockfiles, outdated dependencies, and deployment readiness blockers.
- 🤖 **AI Coding Doctor**: Verifies whether coding tools (**OpenAI Codex**, **Claude Code**, **Google Gemini CLI**, **OpenCode**) and **Model Context Protocol (MCP)** servers are installed, valid, and healthy.
- 🧠 **AI Explain & Local Rules**: Explains runtime errors (`EADDRINUSE`, `ENOENT`, `MODULE_NOT_FOUND`) locally with instant fix suggestions, or optionally via AI providers (**DeepSeek**, **OpenAI**, **OpenRouter**, **Ollama**).
- 🔄 **Snapshot & Diff**: Export non-sensitive environment metadata into JSON and diff local vs VPS to instantly pinpoint why a project runs locally but fails on a server.

---

## 🌟 5 Core Capabilities

<table>
  <tr>
    <td width="50%">
      <h3>🤖 1. AI Coding &amp; MCP Doctor</h3>
      <p>Diagnose readiness of <b>OpenAI Codex</b>, <b>Claude Code</b>, <b>Gemini CLI</b>, and <b>OpenCode</b>. Validates Model Context Protocol (MCP) servers across OS-specific paths with zero secret exposure.</p>
      <code>npx tern-cli agent</code>
    </td>
    <td width="50%">
      <h3>🩺 2. Project Health &amp; Safe Auto-Fix</h3>
      <p>Checks Node versions, lockfiles, <code>.env</code> vs <code>.env.example</code> parity, and deployment readiness. Automatically repairs safe issues (creates missing <code>.env</code>, updates <code>.gitignore</code>).</p>
      <code>npx tern-cli doctor</code> • <code>npx tern-cli fix</code>
    </td>
  </tr>
  <tr>
    <td width="50%">
      <h3>🔌 3. Port Conflict Inspector &amp; Killer</h3>
      <p>Cross-platform port inspection. See which PID and process is hogging port 3000, 5173, or 8080 and safely terminate it with one command.</p>
      <code>npx tern-cli port 3000 --kill</code>
    </td>
    <td width="50%">
      <h3>🔄 4. Environment Snapshot &amp; VPS Diff</h3>
      <p>Capture non-sensitive environment metadata into JSON and diff local vs VPS to solve the classic <i>"works on my machine, fails on VPS"</i> nightmare.</p>
      <code>tern diff local.json server.json</code>
    </td>
  </tr>
  <tr>
    <td colspan="2">
      <h3>💡 5. Local Error Explanations + AI Remediation</h3>
      <p>Instant human-friendly explanations for common developer errors (<code>EADDRINUSE</code>, <code>ENOENT</code>, <code>MODULE_NOT_FOUND</code>, detached Git HEAD) locally without calling external APIs, with optional AI fallback.</p>
      <code>tern why "EADDRINUSE: address already in use :::3000"</code>
    </td>
  </tr>
</table>

---

## 🚀 All Commands at a Glance

| Command | One-Line Summary | Quick Example |
| :--- | :--- | :--- |
| `tern doctor` | Comprehensive project health scan | `tern doctor --strict` |
| `tern agent` | Diagnose AI coding agents &amp; MCP servers | `tern agent --mcp` |
| `tern fix` | Automatically repair safe environment issues | `tern fix` |
| `tern port <port>` | Inspect process on port, optionally terminate | `tern port 3000 --kill` |
| `tern why <error>` | Explain errors locally or with AI | `tern why "EADDRINUSE"` |
| `tern snapshot` | Export non-sensitive environment metadata to JSON | `tern snapshot -o env.json` |
| `tern diff <s1> <s2>` | Diff environments (local vs VPS) | `tern diff local.json vps.json` |
| `tern watch` | Debounced file watcher for config changes | `tern watch` |
| `tern env` | Compare `.env` against `.env.example` safely | `tern env` |
| `tern deploy` | Validate deployment readiness &amp; blockers | `tern deploy` |
| `tern clean` | Free disk space by clearing caches &amp; build folders | `tern clean --dry-run` |
| `tern deps` | Audit dependencies, unpinned versions, vulnerabilities | `tern deps` |
| `tern git` | Check Git status and scan for leaked secrets | `tern git` |
| `tern explain` | AI diagnosis explanation using sanitized report | `tern explain --provider ollama` |
| `tern report` | Generate Markdown report for GitHub Issues | `tern report -o report.md` |

<br />

<details>
<summary><b>📖 Click to expand detailed documentation for all 15 commands</b></summary>
<br />

### 1. `tern doctor`

Scans your developer environment and reports categorized health scores:
- **Fast checks (default)**: Node.js version, lockfiles, Git status, package installation, environment variables consistency, port conflicts, deployment configs, agent instructions, and MCP config syntax.
- **Heavy checks (`--deep`)**: Dependency updates against remote registries and MCP server startup validation.

```bash
# Standard fast check
tern doctor

# Deep check including network audits
tern doctor --deep

# Fail on warnings (exit code 1)
tern doctor --strict

# Output machine-readable JSON for CI pipelines
tern doctor --json
```

---

### 2. `tern agent`

Inspects AI coding environment readiness across platforms:
- **Coding Agents**: Detects installation, version, and configuration for Codex, Claude Code, Gemini CLI, and OpenCode.
- **MCP Servers**: Scans project and OS-level configurations for valid executables, transport types (`stdio`, `sse`), duplicate definitions, and missing environment variables.
- **Agent Instructions**: Verifies presence of `AGENTS.md`, `CLAUDE.md`, and `GEMINI.md`.

```bash
# Full agent environment scan
tern agent

# Inspect MCP servers only
tern agent --mcp

# Machine-readable JSON
tern agent --json

# Fail if any warning or error is present (exit code 1)
tern agent --strict
```

---

### 3. `tern explain`

Explains diagnosed issues using AI. Tern generates a **sanitized diagnostic payload** containing only runtime metadata (Node version, OS, framework) and check messages. **No environment values, source code, or credentials are sent.**

Supported AI providers:
- **DeepSeek** (`DEEPSEEK_API_KEY`)
- **OpenAI-compatible** (`OPENAI_API_KEY`, optional `OPENAI_BASE_URL`)
- **OpenRouter** (`OPENROUTER_API_KEY`, optional `OPENROUTER_BASE_URL`)
- **Ollama** (Local endpoint, default: `http://127.0.0.1:11434`)

```bash
# Auto-detects configured provider from environment
tern explain

# Explicit provider
tern explain --provider deepseek
tern explain --provider openai
tern explain --provider ollama

# Output explanation in JSON
tern explain --json
```

---

### 4. `tern why <error>`

Explains developer errors using a built-in local rule engine:
- `EADDRINUSE` (detects occupying port and process PID)
- `MODULE_NOT_FOUND` / `Cannot find module`
- `ENOENT` / `no such file or directory`
- `EACCES` / `permission denied` (privileged ports < 1024 or filesystem permissions)
- `command not found`
- `npm peer dependency conflict` (ERESOLVE)
- `Git detached HEAD`
- `missing environment variable`
- `connection refused` (ECONNREFUSED)
- `TypeScript common errors` (TS2304, TS2322, TS2345, TS7006, TS2307)

```bash
# Local explanation (no network/AI required)
tern why "EADDRINUSE: address already in use :::3000"

# Module not found explanation
tern why "Cannot find module 'express'"

# If no local rule matches, delegate to AI
tern why "Webpack compilation failed: unexpected token" --ai
```

---

### 5. `tern snapshot`

Exports an environment snapshot in a stable, non-sensitive JSON schema. Captures OS, architecture, Node version, package manager, Git state, framework, safe dependency ranges, environment variable key names (without values), port states, and config presence:

```bash
# Print snapshot to terminal
tern snapshot

# Save snapshot to file
tern snapshot -o local.json
```

---

### 6. `tern diff <source> <target>`

Compares two environment snapshots to isolate discrepancies between machines (e.g. laptop vs VPS):
- **Informational**: Architecture (arm64 vs x64), OS platform.
- **Warnings**: Minor Node or package manager version differences.
- **Blocking**: Major Node version mismatches, missing required environment variables, or port conflicts.

```bash
# Visual table output
tern diff local.json vps.json

# Machine-readable JSON output
tern diff local.json vps.json --json
```

---

### 7. `tern watch`

Monitors project configuration files (`.env`, `.env.example`, `package.json`, lockfiles, MCP configs, `AGENTS.md`, `Dockerfile`) with debouncing, reporting changes cleanly without terminal spam.

```bash
tern watch

# Custom debounce interval (milliseconds)
tern watch --debounce 500
```

---

### 8. `tern fix`

Applies automated repairs to safe-to-fix issues:
- Creates missing `.env` from `.env.example` with placeholder keys.
- Appends missing keys into existing `.env` files.
- Adds `.env` ignore patterns to `.gitignore`.
- Removes accidentally committed `.env` files from Git index (`git rm --cached`).

```bash
# Interactive mode
tern fix

# Non-interactive mode (for CI/CD)
tern fix --yes
```

---

### 9. `tern env`

Compares `.env` against `.env.example` **without displaying or logging variable values**:

```bash
# Compare .env with .env.example
tern env

# Append missing placeholder keys to your local .env
tern env --sync

# Custom paths
tern env --example .env.template --env .env.local
```

---

### 10. `tern port <number>`

Inspects processes occupying a port across macOS, Linux, and Windows:

```bash
# Inspect port 3000
tern port 3000

# Terminate process with confirmation
tern port 3000 --kill

# Force terminate without confirmation
tern port 3000 --kill --force --yes
```

For Docker containers and WSL2 mirrored networking (where `wslhost.exe` or Docker proxies hold the port), see the [Docker & WSL2 port conflicts recipe](docs/recipes/docker-wsl2-ports.md).

---

### 11. `tern clean`

Clears build artifacts and caches (`node_modules/.cache`, `dist`, `build`, `.next`, `.turbo`, `.nuxt`, `coverage`, etc.):

```bash
# Calculate reclaimable disk space without deleting
tern clean --dry-run

# Delete caches with confirmation
tern clean

# Skip confirmation prompt
tern clean --yes

# Also include node_modules root
tern clean --all
```

---

### 12. `tern deps`

Analyzes dependencies for wildcard versions and outdated packages:

```bash
tern deps

# Attempt automated vulnerability remediation
tern deps --fix
```

---

### 13. `tern git`

Examines Git repository health and scans working tree and commits for leaked credentials:

```bash
tern git
```

*Scans for AWS keys, GitHub tokens, Slack tokens, Stripe keys, Private Key blocks, and Google API keys. All detected values are automatically redacted in the output.*

---

### 14. `tern deploy`

Pre-flight verification before production deployments:
- Validates Dockerfile, `vercel.json`, and `netlify.toml` syntax.
- Checks that `.env.production` is ignored in Git.
- Scans source files for hardcoded `http://localhost:` or `http://127.0.0.1:` URLs.
- Verifies that `build` script is declared in `package.json`.

```bash
tern deploy
```

---

### 15. `tern report`

Generates a Markdown report with categorized health breakdown ready to paste into GitHub Issues:

```bash
# Output to stdout
tern report

# Save directly to file
tern report -o tern-report.md
```

</details>

---

## 🔒 Security & Privacy

Tern is designed with a strict security-first architecture:

1. **Local by Default**: All diagnostics, rule-matching, git inspections, port checks, and snapshot collections run 100% locally on your machine.
2. **Opt-in AI Features**: AI features (`tern explain`, `tern why --ai`) are strictly opt-in and only run when invoked by the user.
3. **Strict Sanitization**: When AI features are used, Tern transmits only structured diagnostic metadata (Node version, OS platform, framework, and sanitized issue messages). It never sends `.env` file contents, API keys, credentials, tokens, private keys, or source code files.
4. **Centralized Redaction**: Every output channel (terminal, markdown report, snapshot, and AI requests) passes through centralized redaction filters that scrub database connection passwords, GitHub tokens, AWS keys, JWTs, and private keys.
5. **No Plaintext Secrets in Config**: Tern does not store API keys in project configuration files (`.ternrc.json`). API keys are read directly from environment variables (`DEEPSEEK_API_KEY`, `OPENAI_API_KEY`, `OPENROUTER_API_KEY`).

---

## ⚙️ Configuration (`.ternrc.json`)

Customize Tern's behavior with a `.ternrc.json` file in your project root:

```json
{
  "ignoreChecks": [
    "port-conflicts"
  ],
  "ports": [3000, 5173, 8080],
  "minNodeVersion": ">=18.0.0",
  "cleanPaths": [
    "dist",
    ".next",
    ".cache"
  ],
  "strict": false
}
```

---

## 🛠️ CI / CD Integration

Use Tern in GitHub Actions to catch environment misconfigurations before merging:

```yaml
name: Environment Doctor

on: [push, pull_request]

jobs:
  doctor:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: pnpm/action-setup@v4
        with:
          version: 9
      - uses: actions/setup-node@v4
        with:
          node-version: 22
          cache: 'pnpm'
      - run: pnpm install --frozen-lockfile
      - run: npx tern doctor --strict
      - run: npx tern agent --strict
```

---

## 🤝 Contributing

Contributions are welcome!

1. Clone repository: `git clone https://github.com/terngg/tern.git`
2. Install dependencies: `pnpm install`
3. Run tests: `pnpm test`
4. Run linter: `pnpm lint`
5. Build: `pnpm build`
6. Open a Pull Request!

---

## 💬 Community & Feedback

Have ideas, questions, or diagnostic results to share?
- Join the discussion in [GitHub Discussions](https://github.com/terngg/tern/discussions)
- Report issues or request checks via [GitHub Issues](https://github.com/terngg/tern/issues)
- Review our [Contributing Guide](CONTRIBUTING.md)

---

## 📄 License

[MIT](LICENSE) © 2026 Tern Authors
