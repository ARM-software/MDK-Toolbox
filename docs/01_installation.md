# Installation

There are three ways how to install the MDK-Toolbox. The first two can be used to install the tools on the command line,
while the third approach is used in the Visual Studio Code GUI.

1. [Using vcpkg](#using-vcpkg) - a free C/C++ package manager for acquiring and managing libraries.
2. [Direct access](#direct-access) via curl or wget.
3. [Using an extension](#using-an-extension) in VS Code.

## Using vcpkg

[vcpkg](https://vcpkg.io/en/index.html) is runs on all platforms, build systems, and work flows.

### Installation

If you have not done it before, install `vcpkg` by typing the following at the appropriate command line.

**Windows command shell**

```shell
curl -LO https://aka.ms/vcpkg-init.cmd && .\vcpkg-init.cmd
```

**Windows PowerShell**

```shell
iex (iwr -useb https://aka.ms/vcpkg-init.ps1)
```

**macOS/Linux terminal**

```shell
. <(curl https://aka.ms/vcpkg-init.sh -L)
```

### Initialization

Initialize `vcpkg` by typing the following at the appropriate command line.

**Windows command shell**

```shell
%USERPROFILE%\.vcpkg\vcpkg-init.cmd
```

**Windows PowerShell**

```shell
. ~/.vcpkg/vcpkg-init.ps1
```

**macOS/Linux terminal**

```shell
. ~/.vcpkg/vcpkg-init
```

### Update vcpkg registry

Update the Arm registry to get access to tools using `vcpkg`:

```shell
vcpkg-shell x-update-registry arm
```

Enable the MDK-Toolbox:

```shell
vcpkg-shell use mdk-toolbox
```

## Direct access

The MDK-Toolbox is available for download in the [Arm Tools Artifactory](https://artifacts.tools.arm.com/mdk-toolbox/).
Download the right compressed archive for your host operating system:

**Windows command shell**

```shell
curl --output mdk-toolbox-windows-amd64.zip https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-windows-amd64.zip
```

**macOS terminal**

```shell
curl --output mdk-toolbox-darwin-amd64.tar.gz https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-darwin-amd64.tar.gz
```

**Linux terminal**

```shell
curl --output mdk-toolbox-linux-amd64.tar.gz https://artifacts.tools.arm.com/mdk-toolbox/1.0.0/mdk-toolbox-linux-amd64.tar.gz
```

1. Unzip the file.
2. Set your `PATH` variable to the `bin` directory of the unzipped package.

## Using an extension

The [Arm Environment Manager extension](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) for Visual Studio Code is using vcpkg for tools installation. It already ships with the package manager so that there is no need for the user to manually install vcpkg.

In a CMSIS Solution project, create a file called `vcpkg_configuration.json` that controls the download of additional tools. Add the following:

- Add the Arm artifactory registry to the list of registries:

```json
{
    "name": "arm",
    "kind": "artifact",
    "location": "https://artifacts.tools.arm.com/vcpkg-ce-registry/registry.zip"
}
```

- Add the mdk-toolbox in the requirement list:

```json
"arm:mdk-toolbox": "^1.0.0"
```

Refer to the [Arm Environment Manager documentation](https://marketplace.visualstudio.com/items?itemName=Arm.environment-manager) for more information.
