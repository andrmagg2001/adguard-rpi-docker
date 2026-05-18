# Contributing

Thanks for taking the time to contribute! All contributions are welcome — from fixing a typo to adding support for new hardware.

## How to contribute

### Reporting a bug

Open an issue using the **Bug Report** template. Include:
- Your Raspberry Pi model and OS version
- Docker and Docker Compose versions (`docker --version`, `docker compose version`)
- The exact error message or unexpected behavior
- Steps to reproduce

### Suggesting an improvement

Open an issue using the **Feature Request** template. Explain what you want and why it would help others.

### Submitting a pull request

1. Fork the repository
2. Create a branch: `git checkout -b fix/what-you-fixed`
3. Make your changes
4. Test that `docker compose up -d` works cleanly from scratch
5. Open a pull request with a clear description of what changed and why

## What we welcome

- Support for additional hardware (NUC, VPS, ARM variants)
- Improved blocklist recommendations
- Translations of the README
- Troubleshooting entries based on real issues
- Docker Compose improvements (healthchecks, resource limits)

## Guidelines

- Keep changes focused — one thing per PR
- Update the README if your change affects setup steps
- Don't commit `adguard-conf/` or `adguard-work/` — they contain local data
