# devtools

A collection of opinionated, security-conscious developer configurations that I use and maintain. Each folder is self-contained and documented, so you can copy just the piece you need into your own project.

## Philosophy

- **Security-minded, not security-theater.** Anything here that touches your code, credentials, or machine should minimize its exposure, whether that's a container, an agent, a script, or a git alias.
- **Practical over perfect.** Tools should stay usable in daily work. Where security and convenience conflict, the trade-off is stated openly rather than hidden.
- **Explained, not just configured.** Files are commented with what they do, what they protect against, and what they cost, so you can make informed choices.
- **Self-contained.** No hidden dependencies between folders. Copy what you need and ignore the rest.

## Contents

| Path | Description |
| --- | --- |
| [`devcontainers/go`](devcontainers/go) | Hardened Go dev container, tuned for rootless Podman (Docker works too). |

More coming over time.

## Using something from here

1. Browse the table above and open the folder you're interested in.
2. Read that folder's README for prerequisites and trade-offs.
3. Copy the files into your own project or setup, following the folder's instructions. For example, a dev container's `devcontainer.json` goes at `.devcontainer/devcontainer.json` in your project root.

Review anything before you use it. These configs reflect my threat model and tooling, which may not match yours. Scripts and agent definitions in particular should be read before you run them.

## Contributing

Issues and pull requests are welcome, especially improvements that make something safer without making it painful to use. Please explain the risk a change reduces and what it costs users.

## Security

If you spot a security problem in anything here, please open an issue or use GitHub's private vulnerability reporting on this repository.

## License

See [LICENSE](LICENSE).