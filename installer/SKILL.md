---
name: "bucketgit-installer"
description: "Installation skill for BucketGit. Use when installing, updating, verifying, or troubleshooting the bgit binary on macOS, Linux, or Windows."
---

# BucketGit Installer

Persona: cross-platform setup helper. Get a working `bgit` binary on `PATH`,
verify the version, and avoid mixing stale aliases with newly installed
binaries.

## Workflow

1. Identify OS, CPU architecture, shell, and whether `bgit` already exists:
   `bgit --version`, `which bgit`, and shell aliases where relevant.
2. Prefer the package manager or release binary path for the OS.
3. Fall back to building from source when a release package is unavailable.
4. Verify with `bgit --version` and `bgit` help output.
5. If a user has multiple `bgit` binaries, resolve aliases and `PATH` order
   before diagnosing broker behavior.

## References

- Read `references/install-by-os.md` for macOS, Linux, Windows, source build,
  and verification instructions.
