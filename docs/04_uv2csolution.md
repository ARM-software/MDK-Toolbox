# uvprojx converter uv2csolution

The **uv2csolution** project file converter allows users of µVision to migrate to the new project format CMSIS solution required by CMSIS-Toolbox.

## Usage

```text
Usage:
  uv2csolution <project.uvprojx | multiproject.uvmpw> | [flags]

Flags:
  -d, --dir string   Change output directory for csolution.yml and vcpkg-configuration.json file (e.g. ../ for parent directory)
  -h, --help         Print usage
  -V, --version      Print version
```

### Optimization level conversion

As the CMSIS-Toolbox supports multiple toolchains (Arm Compiler, IAR, GCC, LLVM), the [`optimize:` node](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#optimize) has "generic" levels rather than toolchain specific command line flags. When mapping from µVision, multiple values need to be mapped to a single YML value.

The following table shoes the conversion done by `uv2csolution`:

| µVision | CMSIS Solution |
|---------|----------------|
| -O0, `<default>` | `optimize: none` |
| -O1              | `optimize: none` |
| -O2              | `optimize: speed` |
| -O3              | `optimize: speed` |
| -Ofast           | `optimize: speed` |
| -Os balanced     | `optimize: balanced` |
| -Oz image size   | `optimize: size` |
| -Omax            | `optimize: balanced` |

!!! Attention
    If in µVision **Options for Target - Output - Debug Information** is selected, `optimize: debug` is set to ensure best possible debug experience. Please uncheck that option to enable optimization level conversion based on the table above.

!!! Note
    There is always the possibility to specify toolchain specific command line options using the [`misc:` node](https://open-cmsis-pack.github.io/cmsis-toolbox/YML-Input-Format/#misc) in case the generic abstractions lack granularity.

## Examples

### Simple conversion

```shell
uv2csolution MyProject.uvprojx
```

This step generates the following files:

- `MyProject.csolution.yaml`
- `MyProject.cproject.yaml`
- `vcpkg-configuration.json`

### Multi-project workspace conversion

```shell
uv2csolution MyProject.uvmpw
```

This step generates the following files:

- `MyProject.csolution.yaml`
- `./MyProject1/MyProject1.cproject.yaml`
- `./MyProject2/MyProject2.cproject.yaml`
- More cproject files in separate directories, depending on the number of projects in the multi-project workspace.
- `vcpkg-configuration.json`
