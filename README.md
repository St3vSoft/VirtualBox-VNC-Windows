# VirtualBox VNC for Windows

**A custom Windows build of Oracle VirtualBox with integrated VNC support.**

## Overview

VirtualBox VNC for Windows is a community-maintained custom build of Oracle VirtualBox that enables VNC support through the VirtualBox Remote Desktop Extension (VRDE).

While VNC support is available out of the box on Linux, Windows users do not have an equivalent ready-to-use binary distribution.

This project aims to bridge that gap by integrating the existing VNC implementation into a custom Windows build of VirtualBox, using [libvncserver](https://github.com/LibVNC/libvncserver).

The goal is to allow users to connect directly to their virtual machines using standard VNC clients, such as TigerVNC, RealVNC and TightVNC, without requiring an external VNC server running on the Windows host.

## Features

- Integrated VRDE VNC support for Windows.
- Based on the original Oracle VirtualBox source code.
- Uses libvncserver for VNC functionality.
- Custom Windows MSI installer.
- Compatible with standard VNC clients.
- Guest Additions ISO can be obtained from the official VirtualBox distribution.

## Why this project?

The official VirtualBox distribution for Windows does not provide a ready-to-use VNC-enabled build.

Simply compiling the VNC Extension Pack separately is not sufficient for this particular Windows setup, since the official VirtualBox distribution does not accept the independently built package used in this project.

For this reason, the VirtualBox source code itself needs to be rebuilt with VNC support enabled.

This repository provides the modifications, build configuration and documentation required to reproduce the process.

## Requirements and limitations

This is an unofficial, experimental build.

Please be aware of the following limitations:

- The custom kernel drivers are signed using a test-signing certificate.
- Windows Test Signing Mode is required to load these drivers.
- The corresponding public certificate must be installed.
- Test Signing Mode reduces Windows driver-signing protections.
- The build uses a modified configuration, including `VBOX_WITHOUT_HARDENING`.
- This build is not officially supported by Oracle.


> [!IMPORTANT]
> Do not install certificates or kernel drivers from sources you do not trust. Test-signing configurations should preferably be used on dedicated testing systems.

The public certificate may be distributed alongside the installer, but the private signing key is never included.

## Driver Signing Certificate

The public test-signing certificate used by this build is available in the [certificates](./certificates/) directory.

Windows Test Signing Mode is required to load the custom kernel drivers.

## Downloads

Precompiled Windows MSI installers are available in the [GitHub Releases](../../releases) section.

Each release should include:

- VirtualBox MSI installer.
- Public test-signing certificate (`.CER`).
- Release notes.
- Supported VirtualBox version and Windows compatibility information.

Please read the installation instructions and security requirements before installing.

## Building from source

Building VirtualBox on Windows requires a substantial development environment and several dependencies.

This project uses the following tools:

- Microsoft Visual Studio 2022 Build Tools.
- Windows SDK and WDK.
- Git.
- Python.
- JDK 17
- Qt 6.
- Yasm and NASM.
- Open Watcom.
- WiX Toolset.
- Flex and Bison.
- libvncserver.

The build configuration enables VNC through:

```makefile
VBOX_WITH_EXTPACK_VNC = 1
```

Additional KMK configuration changes are required.

For detailed instructions, see the repository documentation:

- [VirtualBox Build Istructions](https://github.com/St3vSoft/VirtualBox-VNC-Windows/wiki/Building-VirtualBox)
- [Build Environment Setup](https://github.com/St3vSoft/VirtualBox-VNC-Windows/wiki/Build-Environment-Setup)
- [Driver Signing Certificate](https://github.com/St3vSoft/VirtualBox-VNC-Windows/wiki/Build-Environment-Setup)
- [libvncserver Build Istructions](https://github.com/St3vSoft/VirtualBox-VNC-Windows/wiki/Building-libvncserver)

For general VirtualBox build requirements, also consult the [official VirtualBox build instructions](https://www.virtualbox.org/wiki/Build_instructions).

## VNC configuration

VNC access is provided through VirtualBox's VRDE interface.

The VNC server can be configured using VBoxManage, including its authentication password and listening port.

A standard VNC client can then connect to the virtual machine using the configured host address and port.

## Project status

This project is maintained independently and is not affiliated with, endorsed by, or supported by Oracle.

It is intended to provide an alternative Windows build for users who need VNC functionality.

Updates will depend on compatibility with newer VirtualBox versions and the maintenance of the required build modifications.

## License and attribution

This project is based on the original Oracle VirtualBox source code.

VirtualBox base platform packages are distributed under the GNU General Public License, version 3 (GPLv3), subject to the licensing clarifications and additional terms contained in the original `COPYING` file.

Please refer to the original [COPYING](./COPYING) file for complete licensing information, including the conditions applicable to third-party components.

Original copyright notices and attribution must be preserved.

This project does not claim ownership of Oracle VirtualBox or libvncserver.

- [Oracle VirtualBox](https://www.virtualbox.org/)
- [VirtualBox source code](https://github.com/VirtualBox/virtualbox)
- [libvncserver](https://github.com/LibVNC/libvncserver)

---

**Disclaimer:** Oracle and VirtualBox are trademarks of Oracle and/or its affiliates. This is an independent community project and is not an official Oracle product.