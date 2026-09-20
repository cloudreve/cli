# Cloudreve CLI

> [!IMPORTANT]
> Under active development. Features and interfaces may change. Stay tuned for updates.

File management and account controls for Cloudreve. Standalone executables for Linux, macOS, and Windows, available as `cloudreve-cli` and `cr`.

## Install

```sh
mise use -g github:cloudreve/cli@1.0.0
```

[Release archives](https://github.com/cloudreve/cli/releases/latest) include both executable names and SHA-256 checksums. No separate Node.js or Bun installation is required.

## Usage

```sh
cr auth login --server https://cloud.example --email you@example.com
cr ls /my/
cr mkdir /my/Documents
cr cp local:./report.pdf /my/Documents/
cr cp /my/Documents/report.pdf local:./downloaded.pdf
cr ls /my/Documents/ --json
```

Development builds default to local browser login: `cr auth login --server https://cloud.example`. It opens the authorization page and receives its callback on a temporary loopback port. The browser and CLI run on the same computer. `--no-open` prints the URL instead; no code copying is needed. The server must have the built-in Cloudreve CLI OAuth application enabled.

Password login supports email/password and OTP. CAPTCHA requires a supplied answer (and ticket when required) via `--secrets-stdin`; interactive CAPTCHA is handled in the browser. Passwords are prompted securely. Remote paths start at `/my/`; local paths use `local:`. Command help and the [usage reference](docs/usage.md) cover accounts, transfers, scripting, and credential storage.

Cloudreve ≥4.17.0 and <5 is supported through the shared API. CI validates Community 4.19.1, 4.19.0, and 4.18.0. `trash empty` requires 4.18.0 or later.

## Development

[mise](https://mise.jdx.dev/) manages pinned tools. Bun handles dependencies and standalone builds; Node runs the test and package tooling.

```sh
mise install
mise run setup
mise run check
mise run release:build
```

Build and unit checks run on Linux, macOS, and Windows. Real Docker E2E runs use the compiled Linux binary. All production source is included in the 95% coverage minimum for statements, branches, functions, and lines.

[Architecture, tests, and releases](docs/development.md) · [MIT license](LICENSE)
