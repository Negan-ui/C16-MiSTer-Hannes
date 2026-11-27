# Commodore C16 / Plus/4 for MiSTer – Hannes 256K Edition

An enhanced version of the Commodore 264 series FPGA core for MiSTer, adding a Hannes-compatible 256 KiB RAM expansion while retaining the original 64 KiB mode.

The project aims to make software developed for Hannes-expanded Commodore 16 and Plus/4 systems available on MiSTer, including enhanced retro games and homebrew applications.

## Features

- Selectable 64 KiB or 256 KiB (Hannes) RAM in the MiSTer on-screen menu.
- Four 64 KiB RAM banks, implemented using native Cyclone V block RAM. The Hannes expansion provides 256 KiB in total, not 256 KiB in addition to the original 64 KiB.
- Hannes bank switching through register `$FD16`, with selectable common-memory boundaries at `$1000` and `$4000`.
- TED memory-bank selection and standard-bank access.
- No external SDRAM module required for the Hannes expansion.
- C16 and Plus/4 model selection, PAL and NTSC modes, and existing disk, tape, cartridge and optional SID card support inherited from the original core.

## Installation

1. Open the [successful H006 GitHub Actions build](https://github.com/Negan-ui/C16-MiSTer-Hannes/actions/runs/46018176037).
2. Under **Artifacts**, download `C16-Hannes-H006-NativeRAM-results` and extract the ZIP archive.
3. Copy `C16_Hannes_H006_NativeRAM_candidate.rbf` to the `_Computer` directory on your MiSTer SD card.
4. Launch the core from the MiSTer menu.
5. Open the on-screen display and set **RAM** to **256 KiB (Hannes)**.
6. Select **Reset & Apply** and load your Hannes-compatible software.

For conventional software, select **64 KiB** and apply the reset again.

GitHub Actions artifacts have a limited retention period (14 days for this build). Access also requires permission to the repository. If the artifact has expired, a new build is required.

## Development status

**H006 NativeRAM – initial hardware-tested build (27 November 2026)**

The core was successfully compiled with Quartus Prime Lite 17.0.2. Analysis and synthesis, fitting, bitstream generation and timing analysis completed successfully, with zero errors and 66 warnings.

| Test | Result |
| --- | --- |
| Hannes register and bank switching | Passed in HDL simulation |
| Full address-space mapping | Passed in HDL simulation |
| PAL and NTSC TED bus stress tests | Passed in HDL simulation |
| FPGA timing | Setup +0.268 ns, hold +0.224 ns |
| FPGA resources | 37% ALMs, 73% block memory bits, 94% RAM blocks (521/553) |
| Real MiSTer hardware | Successfully tested |
| Adam Is Me Enhanced Edition (256 KiB) | Confirmed running on MiSTer |

This is a hardware-tested development build, not a final compatibility-certified release. Extended gameplay, long-term stability, other Hannes software and complete 64 KiB regression testing remain to be verified. CSORY and larger Hannes expansions are not implemented.

## Building from source

The repository contains the H005 source archive and a GitHub Actions workflow that applies the H006 native block RAM changes, runs the HDL regression tests and builds the RBF with Quartus 17.0.2 and Cyclone V support.

Open **Actions**, select **C16 Hannes H006 - Native block RAM**, and choose **Run workflow**. Build artifacts include the RBF, SHA-256 checksum, simulation logs and Quartus reports.

## Credits and acknowledgements

- **Sorgelig** – original [C16 / Plus/4 MiSTer port](https://github.com/MiSTer-devel/C16_MiSTer), based on upstream snapshot [`25d9d743`](https://github.com/MiSTer-devel/C16_MiSTer/tree/25d9d74366a8ebd0059affa2d1de14f08722ae17).
- **Istvan Hegedus** – original [FPGATED](https://hackaday.io/project/11460-fpgated) TED core.
- **Negan** – Hannes 256 KiB extension project, development and hardware testing.
- Thanks to the MiSTer, Commodore 264 series and LittleSixteen communities, and all contributors to the original core and its dependencies.

## Licensing

This project is based on the existing GPL-licensed MiSTer core. The new Hannes controller carries a GPL-3.0-or-later notice. Original copyright notices and the licenses of individual components must be respected. See the upstream `gpl-3.0.txt` and original file headers. ROM images and third-party software may be subject to separate rights and are not automatically covered by the HDL source licenses.

**Publication status:** This repository is currently private. Its inherited Commodore system and drive ROM images (and the RBF which may embed them) have not been independently cleared for public redistribution. The GPL notice for HDL is not a license for those ROMs. Do not change repository visibility or publish a release until these rights and repository history have been reviewed.

This is an independent community project and is not an official MiSTer-devel release.

Feedback, compatibility reports and contributions are welcome.
