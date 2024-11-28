# Signature creator ElfDwT

[**MDK-Toolbox**](README.md) **&raquo; EflDwT**

The command-line utility **ElfDwT** computes and writes a signature into the application image file. The signature is a
checksum required for NXP devices based on Cortex-M processors and must be used with Flash loaders that do not implement
this computation automatically. The ULINK Family of Debug and Trace Adapters do compute the signature automatically when
used as a Flash loader.

Use the application image file as an argument. The result is written back into the image file. If no BASEADDRESS is
specified, then the base address 0x00 is assumed. For example:

```sh
elfdwt blinky.axf
```

```sh
elfdwt blinky.axf BASEADDRESS(0x1B000000)
```

## Algorithm for creating the checksum

The reserved Cortex-M exception vector location 7 (offset `0x001C` in the vector table) should contain the 2's complement of
the checksum of table entries 0 through 6. This causes the checksum of the first 8 table entries to be 0. The boot loader
code checksums the first 8 locations in sector 0 of the flash. If the result is 0, then execution control is transferred to
the user code.

[**FCARM**](./02_fcarm.md) **&laquo; Chapters &raquo;** [**uv2csolution**](./04_uv2csolution.md)