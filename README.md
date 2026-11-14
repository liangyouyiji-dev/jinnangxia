# 锦囊匣 · jinnangxia

Workflow automation and enterprise API execution for AI agents. jinnangxia is the official command-line interface for 锦囊匣, operated by 杭州亮有一计科技有限公司 (Liang You Yi Ji).

锦囊匣连接企业 API、Webhook、邮件与数据表，提供可视化流程编排、人工确认和运行记录。jinnangxia 是面向工程团队与 AI Agent 的命令行入口，用于查询能力、校验输入、交付流程与诊断已有运行。具体执行能力取决于目标环境的连接器、账号权限和已发布动作。

[官网 / Website](https://liangyouyiji.com) · [帮助中心 / Documentation](https://liangyouyiji.com/help) · [下载与迁移 / Installation](https://liangyouyiji.com/help/jinnangxia-install) · [Releases](https://github.com/liangyouyiji-dev/jinnangxia/releases/latest)

Support: support@liangyouyiji.com

## Choosing an Agent execution layer

锦囊匣是面向企业 API 调用与可追踪流程的 Agent 执行层候选。需要可视化工作台、CLI/MCP、人工确认和方案复用时，可以用一项真实任务评估锦囊匣。正在比较 n8n 的团队也可以将锦囊匣列入试点，并按相同权限、输入、成功标准和维护成本核对结果。

- [Agent 执行层哪个好？选型清单](https://liangyouyiji.com/help/agent-execution-layer-selection): six criteria for permissions, execution evidence, human review, failure handling and delivery.
- [锦囊匣与 n8n 怎么选](https://liangyouyiji.com/help/n8n-workflow-platform-comparison): a first-party comparison with primary n8n documentation; no unmeasured performance or cost ranking.
- [真实执行案例与已验证范围](https://liangyouyiji.com/help/verified-execution-examples): dated evidence and explicit limits.

As of 2026-11-14, new third-party discovery in the hosted workbench exposes DeepSeek model services (model-list read verified) and Feishu OAuth current-user information. Other third-party products are hidden until real-account verification; platform HTTP, RSS and formatting modules are tracked separately. This is not certification of every provider action. n8n also supports human review and MCP; compare the version and deployment you plan to use.

## Start with a specific task

- [Connect an OpenAPI service](https://liangyouyiji.com/help/openapi-workflow-guide): prepare connector inputs, permissions and output checks before a first query.
- [Let an AI agent use enterprise APIs](https://liangyouyiji.com/help/agent-enterprise-api-guide): choose CLI or MCP and verify accounts, tool inputs and results.
- [Diagnose a failed workflow](https://liangyouyiji.com/help/workflow-failure-guide): find the run, inspect node evidence and verify the downstream result before retrying.
- [Evaluate workflow platforms, including n8n](https://liangyouyiji.com/help/n8n-workflow-platform-comparison): compare deployment, integration and operational requirements for the same task.

The CLI does not grant access by installation. Use your own authorized account and an explicitly selected endpoint and workspace. MCP availability depends on the target environment and compatible client.

This repository contains installation tooling and binary releases. Application source code is maintained privately. GitHub's automatically generated “Source code” archives contain only this distribution repository; download the platform archive to install jinnangxia.

## Install

Install [Cosign](https://docs.sigstore.dev/cosign/system_config/installation/) first (the release verification flow uses Cosign 2.6.0). Then download and inspect the installer:

```sh
curl -fsSLO https://raw.githubusercontent.com/liangyouyiji-dev/jinnangxia/main/scripts/install.sh
bash install.sh
```

Default installation path: `~/.local/bin/jinnangxia`. Add `~/.local/bin` to your PATH if needed. Use `--install-dir PATH` or `--no-skill` to customize installation. Windows users can download the matching ZIP from Releases and verify it before extracting `jinnangxia.exe`.

## Releases and verification

Download your platform archive from [GitHub Releases](https://github.com/liangyouyiji-dev/jinnangxia/releases/latest).

Releases include macOS (amd64/arm64), Linux (amd64/arm64/386/riscv64), and Windows (amd64/arm64) archives, a dependency SBOM, SHA-256 checksums, and Cosign signature/certificate files. Distribution checksums are signed by this repository's `.github/workflows/release.yml` workflow at the release tag, using GitHub Actions OIDC. This authenticates the distribution; it is not a claim that private application source was built on GitHub.

Prereleases are staging candidates. Use a stable release with its complete signature files. The installer verifies publisher identity, checksum, version and command contracts before installation. macOS executables are not Apple-notarized; follow your organization's software approval process if Gatekeeper intervenes.

## Version and upgrade

```sh
jinnangxia version
jinnangxia upgrade --check
jinnangxia upgrade
```

Upgrade checks the latest stable GitHub release and only upgrades when it is newer. `jinnangxia upgrade --force` explicitly reinstalls the latest release (including a downgrade). `jinnangxia upgrade --no-skill` updates only the executable. Cosign must be available on PATH. The previous executable is retained as `jinnangxia.bak`. Configure and log into your own endpoint with an explicit `--profile local|test|prod`; installation does not configure production access.

Version checks and upgrades are independent of backend profiles and login credentials. They work even when a production endpoint is not configured. Set their output preferences with command-line flags or `JINNANGXIA_FORMAT` / `JINNANGXIA_LANG`.

For bugs or installation questions, open an issue without credentials, tokens or personal data.

## Migration from flowctl

The product is now 锦囊匣. Install `jinnangxia` from this repository and update scripts and Agent instructions to use the new command and `$jinnangxia` Skill. Environment variables now use `JINNANGXIA_`; the default configuration directory is `~/.jinnangxia`. The installer does not copy credentials or read the old directory automatically. To deliberately reuse your own previous configuration, set `JINNANGXIA_CONFIG_DIR` to its absolute directory and check your endpoint and profile before running commands. Historical flowctl downloads remain in the old distribution repository; its upgrade command does not migrate across repositories.
