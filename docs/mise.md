# Mise

Throng uses [Mise](https://mise.jdx.dev/) to automatically install your project's toolchain dependencies before each Claude Code session starts. You don't need to install or configure Mise yourself — Throng handles that. All you need to do is tell Throng which tools and versions your project requires.

## How Throng uses Mise

When a Claude session is about to start on a task, Throng:

1. Checks your project for a `.tool-versions` (or `mise.toml`) file.
2. Runs `mise install` to ensure every tool and version listed is available in the sandbox.
3. Activates those versions for the session so Claude can run them directly.

This means each task runs with exactly the runtime versions your project expects — Node, Python, Ruby, Go, Terraform, and so on — without you needing to set anything up inside the sandbox.

## The `.tool-versions` file

The simplest way to declare your project's toolchain is a `.tool-versions` file at the root of your repository. It's the same format used by [asdf](https://asdf-vm.com/), so if your project already has one, you don't need to change anything.

Each line lists a tool name followed by a version:

```text
node 20.11.0
python 3.12.2
ruby 3.3.0
go 1.22.1
terraform 1.7.4
```

### Supported version formats

Mise accepts more than just exact versions:

| Format | Example | Meaning |
| --- | --- | --- |
| Exact | `node 20.11.0` | Use this exact version. |
| Fuzzy | `ruby 3` | Latest installed version matching `3.x.x`. |
| Keyword | `node lts` | Latest long-term-support release. |
| Keyword | `python latest` | Latest stable release. |
| Prefix | `go prefix:1.22` | Latest version starting with `1.22`. |
| Ref | `node ref:master` | Build from a VCS ref. |
| Path | `shfmt path:./shfmt` | Use a binary from a local path. |

Comments are supported with `#`.

## Example projects

### Node.js project

```text
node 20.11.0
```

### Python + Node

```text
python 3.12.2
node lts
```

### Polyglot project

```text
ruby 3.3.0
node 20.11.0
python 3.12.2
terraform 1.7.4
```

## Using `mise.toml` instead

If you need more than version pinning — environment variables, tasks, aliases, or tools from registries like npm or pipx — you can use a `mise.toml` file instead. Throng picks this up automatically too.

```toml
[tools]
node = "20.11.0"
python = "3.12"
"npm:@anthropic-ai/claude-code" = "latest"

[env]
NODE_ENV = "development"
```

The `.tool-versions` format is recommended for simple version pinning; `mise.toml` is recommended when you need richer project configuration. See the [Mise configuration docs](https://mise.jdx.dev/configuration.html) for the full reference.

## If your project doesn't have a `.tool-versions` file

Throng will still start a session, but Claude will only have access to the default tools available in the sandbox image. To guarantee the right runtime versions are present, add a `.tool-versions` file at the root of your repository before starting work on a task.

!!! tip "Commit your `.tool-versions` file"
    Check `.tool-versions` (or `mise.toml`) into version control so every Throng session — and every developer on your team — uses the same toolchain.

## Learn more

- [Mise documentation](https://mise.jdx.dev/)
- [Configuration reference](https://mise.jdx.dev/configuration.html)
- [Supported tools](https://mise.jdx.dev/plugins.html)
