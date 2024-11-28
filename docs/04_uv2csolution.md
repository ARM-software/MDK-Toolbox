# uvprojx converter uv2csolution

[**MDK-Toolbox**](README.md) **&raquo; uvprojx converter uv2csolution**

The **uv2csolution** project file converter allows users of µVision to migrate to the new project format CMSIS solution required by CMSIS-Toolbox.

## Usage

```
Usage:
  uv2csolution <project.uvprojx | multiproject.uvmpw> | [flags]

Flags:
  -d, --dir string   Change output directory for csolution.yml and vcpkg-configuration.json file (e.g. ../ for parent directory)
  -h, --help         Print usage
  -V, --version      Print version
```

**Examples**

```sh
uv2csolution MyProject.uvprojx --dir ../
```
This step generates the following files in the parent directory:

- `MyProject.csolution.yaml`
- `MyProject.cproject.yaml`
- `vcpkg-configuration.json`

```sh
uv2csolution MyProject.uvmpw
```

This step generates the following files:

- `MyProject.csolution.yaml`
- `./MyProject1/MyProject1.cproject.yaml`
- `./MyProject2/MyProject2.cproject.yaml`
- More cproject files, depending on the number of uvprojx files in the uvmpw file.
- `vcpkg-configuration.json`

[**ElfDwT**](./03_elfdwt.md) **&laquo; Previous Chapter**
