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

### Examples

*Simple conversion*

```shell
uv2csolution MyProject.uvprojx
```

This step generates the following files:

- `MyProject.csolution.yaml`
- `MyProject.cproject.yaml`
- `vcpkg-configuration.json`

*Multi-project workspace conversion*

```shell
uv2csolution MyProject.uvmpw
```

This step generates the following files:

- `MyProject.csolution.yaml`
- `./MyProject1/MyProject1.cproject.yaml`
- `./MyProject2/MyProject2.cproject.yaml`
- More cproject files in separate directories, depending on the number of projects in the multi-project workspace.
- `vcpkg-configuration.json`
