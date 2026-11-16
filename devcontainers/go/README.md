# Go Hardened Dev Container

A security-conscious [Dev Container](https://containers.dev/) for Go, tuned for **rootless Podman** (Docker works too). It shrinks the attack surface of your dev environment while keeping `gopls`, `golangci-lint`, `delve`, and `go build/test` working out of the box.

Part of [devtools](../README.md). This folder is self-contained: copy `.devcontainer/` into your project.

## Quick start

**Prerequisites:** Podman (rootless recommended) or Docker, and VS Code with the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

- **Podman:** set `"dev.containers.dockerPath": "podman"` in your VS Code user settings.
- **Docker:** delete the `--userns=keep-id` line from `runArgs`.

Then copy `.devcontainer/` into your project root and run **Dev Containers: Reopen in Container**.

## What's hardened

Every setting is explained in [`devcontainer.json`](.devcontainer/devcontainer.json), including its trade-offs. In short:

- Non-root container user, all capabilities dropped, `no-new-privileges`, PID limit
- Per-project Go module cache, so one project can't poison another
- `GOTOOLCHAIN=local` and no runtime tool auto-updates, so nothing is silently downloaded
- No container-engine socket mounted, no auto-forwarded ports

`sudo` and `ping` don't work inside the container, by design.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| Permission denied on workspace (SELinux hosts) | Uncomment `workspaceMount` in `devcontainer.json` |
| Delve can't attach | Add `--cap-add=SYS_PTRACE` to `runArgs` |
| Other "operation not permitted" errors | Add back only the specific capability needed with `--cap-add` |
| Wrong file ownership (Podman) | Ensure `--userns=keep-id` is set and Podman is rootless |
| Module cache empty or not writable | Remove the `go-mod-cache-*` volume (`podman volume rm`) and rebuild |

## Limitations

This reduces risk; it doesn't eliminate it.

- **Credentials may be forwarded.** Dev Containers forwards your SSH agent and git credentials by default. This is set in VS Code **user** settings, not here. See the note at the bottom of `devcontainer.json`.
- **The workspace is read-write.** Code in the container can modify project files on your host, so review diffs before committing.
- **Network is open.** Dependencies can make outbound connections.
- **A container is not a VM.** Open untrusted repos in a throwaway environment.

## Contributing

PRs welcome, especially hardening that keeps developer experience intact. Explain the threat mitigated and the cost to developers.

## License

See the repository's [LICENSE](../LICENSE).