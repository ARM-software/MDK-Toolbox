# MDK-Toolbox

The MDK-Toolbox consists of the following utilities:

- **FCARM**, a file converter that reformats web files into a single C source file which is then included and compiled into a project.
- **ElfDwT**, a command-line utility that computes and writes a signature into the application image file.
- **uv2csolution**, a command-line utility that converts µVision projects to [CMSIS solution format](https://github.com/Open-CMSIS-Pack/cmsis-toolbox/blob/main/docs/YML-Input-Format.md).
- **Mbed TLS/cert_write**, an application that signs a certificate signing request, or self-signs a certificate.
- **Mbed TLS/gen_key**, an application that generates a key for any of the supported public-key algorithms (RSA or ECC).

## Installation

There are three ways how to install the MDK-Toolbox. The first two can be used to install the tools on the command line,
while the third approach is used in the Visual Studio Code GUI.

1. [Using vcpkg](#using-vcpkg) - a free C/C++ package manager for acquiring and managing libraries.
2. [Direct access](#direct-access) via curl or wget.
3. [Using an extension](#using-an-extension) in VS Code.

### Using vcpkg

[vcpkg](https://vcpkg.io/en/index.html) is runs on all platforms, build systems, and work flows.

1. If you have not done it before, install vcpkg (otherwise continue to step 2):

   - In a Windows command shell, type:

     ```sh
     curl -LO https://aka.ms/vcpkg-init.cmd && .\vcpkg-init.cmd
     ```

   - In a Windows PowerShell, type:

     ```sh
     iex (iwr -useb https://aka.ms/vcpkg-init.ps1)
     ```

   - In a macOS/Linux terminal, type:

     ```sh
     . <(curl https://aka.ms/vcpkg-init.sh -L)
     ```

2. Initialize vcpkg:

   - In a Windows command shell, type:

     ```sh
     %USERPROFILE%\.vcpkg\vcpkg-init.cmd
     ```

   - In a Windows PowerShell, type:

     ```sh
     . ~/.vcpkg/vcpkg-init.ps1
     ```

   - In a macOS/Linux terminal, type:

     ```sh
     . ~/.vcpkg/vcpkg-init
     ```

3. Update the Arm vcpkg registry (this will give you access to tools hosted by Arm):

   ```shell
   vcpkg-shell x-update-registry arm
   ```

4. Enable the MDK-Toolbox:

   ```shell
   vcpkg-shell use mdk-toolbox
   ```

### Direct access

The MDK-Toolbox is available for download in the **Arm Tools Artifactory** at https://artifacts.tools.arm.com/mdk-toolbox/.

1. Download the right compressed archive for your host operating system:

   - In a Windows terminal, type:

     ```sh
     curl --output mdk-toolbox-windows-amd64.zip https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-windows-amd64.zip
     ```

   - In a macOS terminal, type:

     ```sh
     curl --output mdk-toolbox-darwin-amd64.tar.gz https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-darwin-amd64.tar.gz
     ```

   - In a Linux terminal, type:

     ```sh
     curl --output mdk-toolbox-linux-amd64.tar.gz https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-linux-amd64.tar.gz
     ```

2. Unzip the file.

3. Set your `PATH` variable to the `bin` directory of the unzipped package.

### Using an extension

The [Arm Environment Manager extension](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) for Visual Studio Code is using vcpkg for tools installation. It already ships with the package manager so that there is no need for the user to manually install vcpkg.

In a CMSIS Solution project, create a file called `vcpkg_configuration.json` that controls the download of additional tools.

1. In the `vcpkg_configuration.json` file, the Arm artifactory registry must be added to the list of registries.

   ```json
   {
       "name": "arm",
       "kind": "artifact",
       "location": "https://artifacts.tools.arm.com/vcpkg-ce-registry/registry.zip"
   }
   ```

2. In the vcpkg_configuration.json file, the mdk-toolbox should be added under the requirement list:

   ```json
   "arm:mdk-toolbox": "^1.0.0"
   ```

3. Refer to the [Arm Environment Manager documentation](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) for more information.

## Documentation

The documentation for the MDK-Toolbox utilities can found here:

- [FCARM](https://developer.arm.com/documentation/101407/latest/Appendix/H--File-Converter-FCARM)
- [ElfDwT](https://developer.arm.com/documentation/101407/latest/Utilities/Signature-Creator-for-NXP-Cortex-M-Devices)
- [uv2csolution](https://learn.arm.com/learning-paths/microcontrollers/uvprojx-conversion/how-to-2/)
- [Mbed TLS/cert_write](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-self-signed-certificate/#command-to-generate-a-self-signed-certificate)
- Mbed TLS/gen_key:
  - [RSA key pair generator](https://mbed-tls.readthedocs.io/en/latest/kb/cryptography/rsa-key-pair-generator/)
  - [How to generate a Certificate Request (CSR)](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-certificate-request-csr/)
  - [How to generate a self-signed certificate](https://mbed-tls.readthedocs.io/en/latest/kb/how-to/generate-a-self-signed-certificate/)

## Licenses

The MDK-Toolbox utilities are provided under the following license terms:

- The FCARM, ElfDwT, and uv2csolution tools are provided under the [MDK v6 license agreement](https://www.keil.arm.com/license-agreement/).
- The Mbed TLS tools cert_write and gen_key are provided under the [mbed TLS license argreement](https://github.com/Mbed-TLS/mbedtls/blob/development/LICENSE).
