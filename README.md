# AW1000 Node build-only repository

This public repository is **only for building a review candidate** of Node.js v26.13.0
from the official upstream source, using GitHub-hosted ARM64 and Alpine/musl.

**NO AC INTERNET PREPAID source code, customer information, router firmware,
router libraries, credentials, device keys, or other private assets belong here.**

## Current workflow

- `.github/workflows/build-node-musl.yml` runs on GitHub-hosted `ubuntu-24.04-arm`.
- The Node build runs **inside** a temporary Alpine 3.23 ARM64/musl container.
- `build-inputs/source.sha256` is a pinned checksum supplied from an already
  independently verified signed Node.js source archive.
- The source archive checksum must match before extraction or compilation.
- The output artifact is deliberately labelled **REVIEW-ONLY** and is not a deployable router image.
- A successful GitHub Actions run **does not imply** runtime compatibility on the AW1000
  (OpenWrt 19.07.7, AArch64, Linux 4.19.190) or production readiness.

## After successful build

1. Download the REVIEW-ONLY artifact from the Actions run.
2. Locally compare ELF architecture, dynamic loader (PT_INTERP), DT_NEEDED,
   imported symbols, C library and dependency closure against previously
   collected AW1000 ABI evidence.
3. Independently validate the artifact checksum and check runtime/crypto
   compatibility in a controlled environment.
4. Perform an explicitly approved, temporary, bounded smoke test only after
   preflight checks and review; **no router deployment is authorized**.

## Safety

GitHub Actions cannot access the AW1000 or Dell. This repository never
contains production code or router-specific private files. Do not upload the
router libc or device evidence here.

**ProductionGate = NO-GO.**
