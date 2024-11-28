# Installation

[**MDK-Toolbox**](README.md) **&raquo; Installation**

There are three ways how to install the MDK-Toolbox. The first two can be used to install the tools on the command line,
while the third approach is used in the Visual Studio Code GUI.

1. [Using vcpkg](#using-vcpkg) - a free C/C++ package manager for acquiring and managing libraries.
2. [Direct access](#direct-access) via curl or wget.
3. [Using an extension](#using-an-extension) in VS Code.

## Using vcpkg

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

## Direct access

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

## Using an extension

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

[**Overview**](README.md) **&laquo; Chapters &raquo;** [**FCARM**](./02_fcarm.md)