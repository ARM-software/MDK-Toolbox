# MDK-Toolbox

This repository contains the documentation of the [MDK-Toolbox](https://artifacts.tools.arm.com/mdk-toolbox/) that provides
a set of command-line tools for various purposes.

## Users guide

The [**Users Guide**](./docs/README.md) provides detailed information.

## Included tools

The MDK-Toolbox consists of the following utilities:

- **FCARM**, a file converter that reformats web files into a single C source file which is then included and compiled into a project.
- **ElfDwT**, a command-line utility that computes and writes a signature into the application image file.
- **uv2csolution**, a command-line utility that converts µVision projects to [CMSIS solution format](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md).
- **Mbed TLS/cert_write**, an application that signs a certificate signing request, or self-signs a certificate.
- **Mbed TLS/gen_key**, an application that generates a key for any of the supported public-key algorithms (RSA or ECC).

## Licenses

The MDK-Toolbox utilities are provided under the following license terms:

- The FCARM, ElfDwT, and uv2csolution tools are provided under the
  [MDK v6 license agreement](https://www.keil.arm.com/license-agreement/).
- The Mbed TLS tools cert_write and gen_key are provided under the
  [mbed TLS license argreement](https://github.com/Mbed-TLS/mbedtls/blob/development/LICENSE).
