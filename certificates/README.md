# Test Signing Certificate

This directory contains the public X.509 certificate used to sign the custom VirtualBox Windows kernel drivers.

## Certificate information

- Subject: `VirtualBoxTest`
- Purpose: Windows kernel driver test signing
- Format: X.509 (.CER)

## Installation

The certificate must be installed in the appropriate Windows certificate stores for the test-signing configuration.

**Important:** Installing this certificate alone does not enable test-signed drivers. Windows Test Signing Mode must also be enabled.

Only install this certificate if you trust this project's source and maintainers.

The corresponding private signing key is not included in this repository.