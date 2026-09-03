<p align="center">
  <a href="README.md">English (personal fork)</a> |
  Upstream translations:
  <a href="README.zh.md">简体中文</a> |
  <a href="README.zht.md">繁體中文</a> |
  <a href="README.ko.md">한국어</a> |
  <a href="README.de.md">Deutsch</a> |
  <a href="README.es.md">Español</a> |
  <a href="README.fr.md">Français</a> |
  <a href="README.it.md">Italiano</a> |
  <a href="README.da.md">Dansk</a> |
  <a href="README.ja.md">日本語</a> |
  <a href="README.pl.md">Polski</a> |
  <a href="README.ru.md">Русский</a> |
  <a href="README.bs.md">Bosanski</a> |
  <a href="README.ar.md">العربية</a> |
  <a href="README.no.md">Norsk</a> |
  <a href="README.br.md">Português (Brasil)</a> |
  <a href="README.th.md">ไทย</a> |
  <a href="README.tr.md">Türkçe</a> |
  <a href="README.uk.md">Українська</a> |
  <a href="README.bn.md">বাংলা</a> |
  <a href="README.el.md">Ελληνικά</a> |
  <a href="README.vi.md">Tiếng Việt</a> |
  <a href="README.hi.md">हिन्दी</a>
</p>

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/hero-dark.webp">
    <source media="(prefers-color-scheme: light)" srcset="assets/hero-light.webp">
    <img src="assets/hero-dark.png" alt="CyberStrike open-source offensive security agent" width="880">
  </picture>
</p>

<h3 align="center">Personal fork: an enhanced CyberStrike distribution and operational workbench.</h3>

<p align="center">
  Maintained by <a href="https://github.com/spetro511">Suren Sahayachny (<code>spetro511</code>)</a><br>
  and built on the original open-source project from
  <a href="https://github.com/CyberStrikeus/CyberStrike"><code>CyberStrikeus/CyberStrike</code></a>
  and its contributors.
</p>

<p align="center">
  <a href="#about-this-fork">About this fork</a> &bull;
  <a href="#operational-workbench">Workbench</a> &bull;
  <a href="#using-this-fork">Installation</a> &bull;
  <a href="#upstream-project-and-contributor-credit">Upstream</a> &bull;
  <a href="#ethical-use">Ethical use</a> &bull;
  <a href="#license">License</a>
</p>

<p align="center">
  <a href="https://github.com/spetro511/CyberStrike"><img alt="Personal fork" src="https://img.shields.io/badge/fork-spetro511%2FCyberStrike-1e40af?style=flat-square" /></a>
  <a href="https://github.com/CyberStrikeus/CyberStrike"><img alt="Upstream project" src="https://img.shields.io/badge/upstream-CyberStrikeus%2FCyberStrike-334155?style=flat-square" /></a>
  <a href="https://github.com/CyberStrikeus/CyberStrike/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-AGPL--3.0--only-1e40af?style=flat-square" /></a>
</p>

---

### About This Fork

> [!IMPORTANT]
> CyberStrike originated at
> [**`CyberStrikeus/CyberStrike`**](https://github.com/CyberStrikeus/CyberStrike). This repository is Suren
> Sahayachny's personal fork of that AGPL-licensed open-source project. Suren did **not** create the original
> CyberStrike project; its original authors and contributors retain full credit through the upstream repository and
> Git history.

Suren took the upstream project and substantially enhanced it as an operational distribution for day-to-day,
authorized security work. The main contribution of this fork is an expanded Web UI that acts as a centralized hub
for observing an engagement, understanding its posture, managing evidence, and operating a managed CyberStrike
deployment.

The upstream package, website, documentation, releases, and community remain upstream resources. Features documented
as fork enhancements below may not be present in an upstream release.

---

### Operational Workbench

The fork connects the existing agent, tool, browser, MCP, Bolt, and finding data into one live browser workbench.

| Area                        | Fork enhancement                                                                                                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Central Web UI**          | A session workbench that keeps agent interaction, findings, execution status, and engagement context together instead of treating the browser as a static companion view. |
| **Live activity**           | Durable, redacted engagement events with live updates, correlation data, source filters, timeline and lane views, reconnect recovery, and JSONL export.                   |
| **Mission posture**         | Methodology phase state, per-asset coverage, blockers, warnings, attack-chain candidates, agent performance, and approval-aware next actions.                             |
| **Topology**                | Evidence-linked assets, hosts, services, routes, endpoints, identities, findings, and relationships in a searchable engagement graph.                                     |
| **Nmap workflows**          | Approval-gated scan profiles, exact command previews, canonical XML ingestion, saved scan history, topology projection, and comparisons between scans.                    |
| **Target notes**            | Operator-authored notes attached to topology entities, with links and human-confirmed provenance.                                                                         |
| **Structured memory**       | Project and session memory with working, episodic, semantic, and procedural categories; search, provenance, trust, confidence, redaction, and invalidation.               |
| **Observer access**         | A server-enforced read-only role for redacted activity, mission, topology, findings, and status data without mutation, secret, raw-event, PTY, or configuration access.   |
| **Managed Kali deployment** | Target-selectable source builds, installation of the matching HackBrowser worker and Web UI, and a localhost-only `systemd` user service template.                        |

The implementation is visible in the
[session workbench UI](./packages/app/src/pages/session/),
[server routes](./packages/cyberstrike/src/server/routes/),
[topology and Nmap model](./packages/cyberstrike/src/topology/), and
[structured memory store](./packages/cyberstrike/src/memory/).

#### Operational flow

```text
Authorized engagement
        |
        v
CyberStrike agent and tools -----> durable, redacted activity
        |                                      |
        +--> Mission posture                   +--> Web UI timeline and lanes
        +--> Nmap evidence --> Topology
        +--> Findings and target notes
        +--> Structured project/session memory

Operator: full authenticated control
Observer: redacted read-only projection
```

---

### Using This Fork

#### Upstream release

The published package is maintained by the upstream project:

```bash
npm i -g @cyberstrike-io/cyberstrike@latest
cyberstrike
```

See the [upstream documentation](https://docs.cyberstrike.io) for its supported release workflow. The npm package
does not necessarily include enhancements that exist only on this fork.

#### Build and deploy the fork on Kali/Linux

Source deployments require the compiled binary, matching HackBrowser worker, and Web UI bundle. Use the
repository-pinned Bun version:

```bash
bun install --frozen-lockfile
bun run --cwd packages/app build
CYBERSTRIKE_BUILD_TARGET=linux-x64 bun run --cwd packages/cyberstrike script/build.ts

# Installs the binary and its sibling HackBrowser worker.
./install --binary packages/cyberstrike/dist/cyberstrike-linux-x64/bin/cyberstrike

# Installs the locally built Web UI.
install -d "${XDG_DATA_HOME:-$HOME/.local/share}/cyberstrike/web"
cp -R packages/app/dist/. "${XDG_DATA_HOME:-$HOME/.local/share}/cyberstrike/web/"

CYBERSTRIKE_SERVER_PASSWORD=change-me cyberstrike web --hostname 127.0.0.1
```

Use `linux-x64-baseline` on x64 CPUs without AVX2, or the corresponding `*-musl` target on musl-based
distributions. Back up the installed binary, configuration, and data directory before replacing a managed
deployment.

For a persistent localhost-only service, install
[`contrib/systemd/cyberstrike-web.service`](./contrib/systemd/cyberstrike-web.service) under
`~/.config/systemd/user/`. Create a mode `0600` file at `~/.config/cyberstrike/web.env` containing
`CYBERSTRIKE_SERVER_PASSWORD`, then run:

```bash
systemctl --user daemon-reload
systemctl --user enable --now cyberstrike-web.service
```

#### Remote access and observers

Keep the service bound to localhost and use an authenticated SSH or Cloudflare tunnel rather than exposing port
`4096` directly.

```bash
export CYBERSTRIKE_SERVER_PASSWORD=your-operator-password
export CYBERSTRIKE_OBSERVER_PASSWORD=your-read-only-password
cyberstrike web --hostname 127.0.0.1
```

The optional `observer` credential is restricted by server policy. It is suitable for monitoring redacted engagement
state, not for controlling agents or accessing secrets. If user or project configuration prevents startup,
`cyberstrike web --safe` starts recovery mode without those configuration sources; managed administrator policy is
still enforced.

---

### Upstream Project and Contributor Credit

This fork exists because of the original CyberStrike project and the work of its maintainers and community.

| Resource                  | Link                                                                                     |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| **Original repository**   | [CyberStrikeus/CyberStrike](https://github.com/CyberStrikeus/CyberStrike)                |
| **Upstream contributors** | [Contributor history](https://github.com/CyberStrikeus/CyberStrike/graphs/contributors)  |
| **Documentation**         | [docs.cyberstrike.io](https://docs.cyberstrike.io)                                       |
| **Website**               | [cyberstrike.io](https://cyberstrike.io)                                                 |
| **Published package**     | [@cyberstrike-io/cyberstrike](https://www.npmjs.com/package/@cyberstrike-io/cyberstrike) |
| **Releases**              | [Upstream releases](https://github.com/CyberStrikeus/CyberStrike/releases)               |
| **Issues and roadmap**    | [Upstream issues](https://github.com/CyberStrikeus/CyberStrike/issues)                   |
| **Community**             | [Discord](https://discord.gg/snunAaHf6U)                                                 |

Git history is intentionally preserved so upstream and fork contributors remain attributed for their work. For
changes intended for the original project, read the [Contributing Guide](./CONTRIBUTING.md) and submit them to the
upstream repository. Fork-specific work should be proposed to
[`spetro511/CyberStrike`](https://github.com/spetro511/CyberStrike) against the appropriate personal-fork branch.

---

### Ethical Use

CyberStrike is intended only for systems you own or are explicitly authorized to test. Users are responsible for
scope, approvals, data handling, tool execution, and compliance with applicable laws and engagement rules.

The agent is **not a security sandbox**. Review commands and active-test previews before approving them, protect
credentials, and do not expose the Web UI directly to untrusted networks. Read the
[Code of Conduct and ethical-use policy](./CODE_OF_CONDUCT.md) and [Security Policy](./SECURITY.md) before operating
the software.

---

### License

The upstream project and this fork are distributed under the
[GNU Affero General Public License v3.0 only](./LICENSE) (`AGPL-3.0-only`). Fork modifications remain under the same
license and do not replace or weaken upstream copyright or contributor attribution.

The upstream project also advertises commercial licensing through
[contact@cyberstrike.io](mailto:contact@cyberstrike.io).

---

<p align="center">
  <a href="https://github.com/CyberStrikeus/CyberStrike"><b>Original CyberStrike project</b></a> ·
  <a href="https://github.com/spetro511/CyberStrike"><b>Suren's personal fork</b></a> ·
  <a href="https://docs.cyberstrike.io"><b>Upstream docs</b></a> ·
  <a href="https://cyberstrike.io"><b>Upstream website</b></a>
</p>
<p align="center">
  <sub>Upstream CyberStrike and its contributors are the foundation of this enhanced personal distribution.</sub>
</p>
