# MDK-Toolbox user's guide

The MDK-Toolbox consists of the following utilities:

- **FCARM**, a file converter that reformats web files into a single C source file which is then included and compiled into a project.
- **ElfDwT**, a command-line utility that computes and writes a signature into the application image file.
- **uv2csolution**, a command-line utility that converts µVision projects to [CMSIS solution format](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md).
- **Mbed TLS/cert_write**, an application that signs a certificate signing request, or self-signs a certificate.
- **Mbed TLS/gen_key**, an application that generates a key for any of the supported public-key algorithms (RSA or ECC).

## Manual chapters

- [Installation](./01_installation.md)
- [FCARM](./02_fcarm.md)
- [ElfDwt](./03_elfdwt.md)
- [uv2csolution](./04_uv2csolution.md)
- [Licenses](./licenses.md)

## External documentation

- [Mbed TLS/cert_write](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-self-signed-certificate/#command-to-generate-a-self-signed-certificate)
- Mbed TLS/gen_key:
  - [RSA key pair generator](https://mbed-tls.readthedocs.io/en/latest/kb/cryptography/rsa-key-pair-generator/)
  - [How to generate a Certificate Request (CSR)](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-certificate-request-csr/)
  - [How to generate a self-signed certificate](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-self-signed-certificate/)
