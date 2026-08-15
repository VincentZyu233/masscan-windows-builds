# Masscan Windows Builds

[![Build](https://github.com/VincentZyu233/masscan-windows-builds/actions/workflows/build.yml/badge.svg)](https://github.com/VincentZyu233/masscan-windows-builds/actions/workflows/build.yml)

This repository provides reproducible Windows x64 builds and a dedicated Scoop bucket for [Masscan](https://github.com/robertdavidgraham/masscan).

This is an independent distribution project and is not affiliated with or endorsed by the upstream Masscan project. Builds use an official upstream source archive pinned by SHA-256. Build logs, artifacts, release checksums, and GitHub artifact attestations are public.

## Install with Scoop

Masscan requires [Npcap](https://npcap.com/) on Windows. Install and enable Npcap before running a scan; this package does not bundle or redistribute it.

```powershell
scoop bucket add masscan-windows https://github.com/VincentZyu233/masscan-windows-builds
scoop install masscan-windows/masscan
```

Verify the installation without sending scan traffic:

```powershell
masscan --echo
masscan --version
masscan --iflist
```

Some Masscan versions print valid `--version` output but exit with status code `1`. This does not by itself mean that the executable is broken; `--echo` is the primary no-scan health check used by this repository.

## Build provenance

- Upstream source: `robertdavidgraham/masscan`
- Upstream version: `1.3.2`
- Target: Windows x64 with MinGW-w64
- License: AGPL-3.0-only

The workflow first supports a non-publishing artifact build. A release is created only when the workflow is manually dispatched with `publish` enabled.

## Build from upstream source

```powershell
scoop install git gcc make
git clone --branch 1.3.2 --depth 1 https://github.com/robertdavidgraham/masscan.git
cd masscan
make
```

The resulting executable is located at `bin\masscan.exe`. Npcap is still required at runtime.

## Security

Masscan can generate traffic at a very high rate. Only scan systems and networks for which you have explicit authorization, and set a conservative rate appropriate for the target environment.
