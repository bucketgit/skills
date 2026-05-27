# Install By OS

## macOS

Preferred path:

```bash
brew tap bucketgit/bgit
brew install bgit
bgit --version
```

Upgrade:

```bash
brew update
brew upgrade bgit
bgit --version
```

If behavior differs between shells, check aliases and path order:

```bash
which bgit
type bgit
unalias bgit
```

## Linux

Use the published release binary for the target architecture when available.
Install it somewhere on `PATH`, commonly `/usr/local/bin/bgit`:

```bash
chmod +x bgit
sudo mv bgit /usr/local/bin/bgit
bgit --version
```

If the user cannot use `sudo`, install under `~/.local/bin` and ensure that
directory is on `PATH`:

```bash
mkdir -p ~/.local/bin
mv bgit ~/.local/bin/bgit
chmod +x ~/.local/bin/bgit
bgit --version
```

## Windows

Use the Windows release binary when available. Put `bgit.exe` in a directory on
`PATH`, then verify from PowerShell:

```powershell
bgit --version
where.exe bgit
```

For source builds, install Go and build from a Git checkout:

```powershell
git clone https://github.com/bucketgit/bgit.git
cd bgit
go build -o bgit.exe .
.\bgit.exe --version
```

## Build From Source

Works on macOS, Linux, and Windows with Go installed:

```bash
git clone https://github.com/bucketgit/bgit.git
cd bgit
go build -o bgit .
./bgit --version
```

Use this path for unreleased development builds, local patches, or CI-generated
artifacts.

## Post-Install Checks

```bash
bgit --version
bgit
bgit setup --help
```

If `bgit --version` is not the expected version, inspect aliases, shell hash
caches, and duplicate binaries before changing brokers.
