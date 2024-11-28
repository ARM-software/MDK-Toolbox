# File Converter fcarm

[**MDK-Toolbox**](README.md) **&raquo; FCARM**

This file converter reformats all web files into a single C-file which is then included and compiled into the project.

fcarm is invoked from the command line and has the syntax:

```sh
fcarm @commandfile
```

Where

`commandfile` is the name of a command file that can contain an inputlist, outputfile, and directives. (See below.)

or

```sh
fcarm {inputlist} TO {outputfile} {directives}
```

Where

- `inputlist` is a comma-separated list of files. The files get converted into one output file. Filenames must be specified
  with the file extension, but without the path information.
- `outputfile` name of the output C-file containing the converted web files.
- `directives` commands and parameters that control the operation of the file converter. Available directives:

   | Directive  | Description                                                                                                   |
   | ---------- | ------------------------------------------------------------------------------------------------------------- |
   | [PRINT](#print)           | Specify the name of the listing file. Default is the base name of the output C-file with the extension *.LST. |
   | [NOPRINT](#noprint)       | Disables generation of the listing (LST) file.                                                                |
   | [PAGEWIDTH](#pagewidth)   | Specifies the number of characters on a line in the listing file.                                             |
   | [PAGELENGTH](#pagelength) | Specifies the number of lines on a page in the listing file.                                                  |
   | [ROOT](#root)             | Specifies the root path where web files are located relative to the project directory path.                   |

In addition to the output file, fcarm generates a listing file with the base name of the output file and the extension *.LST.

## Optimization

fcarm integrates a file optimization algorithm to compress files and creates more compact and smaller executable images.
fcarm decides on the file extension which kind of compression is used. Each file group has a different compression and
optimization flavor.

When the filename has the tilde prefix (for example, ~doStuff.js) then compression or certain compression optimizations
are disabled. This is useful when debugging a file. It is hard to trace code compacted to a single line with no spaces,
no comments, and no line feeds.

Compression and optimization is performed in two iterations. In a 2nd pass, further optimization is performed resulting
in better code density.

<table>
    <thead>
        <tr><th>Group</th><th>Extension</th><th>Optimization</th><th>~Optimization
                (disabled)</th></tr>
    </thead>
    <tbody>
        <tr>
            <td>HTML</td>
            <td>html<br>htm<br>inc</td>
            <td><b>HTML compression</b><br> Performs the following
                optimizations:
                <ul>
                    <li>replaces tab characters with spaces</li>
                    <li>removesline-termination CR-LF characters</li>
                    <li>replacesmultiple spaces with a single space</li>
                    <li>removes leading and trailing spaces</li>
                    <li>removes space between two html tags (for example,
                        "&lt;ul&gt; &lt;li&gt;")</li>
                </ul>
            </td><td>no compression</td>
        </tr>
        <tr>
            <td>CGI</td>
            <td>cgi<br> cgx</td>
            <td><b>CGI compression</b><br>Optimizes scripts for maximum
                performance on TCPnet web server:
                <ul>
                    <li>checks the script syntax</li>
                    <li>replaces T,C,I,# script commands with tokens</li>
                    <li>replaces tab characters with spaces</li>
                    <li>removes line-termination CR-LF characters</li>
                    <li>removes multiple spaces</li>
                    <li>removes comments from script lines</li>
                    <li>groups small t-commands</li>
                </ul>
            </td>
            <td>white space removal but without grouping of small
                t-commands</td>
        </tr>
        <tr>
            <td>CSS</td>
            <td>css</td>
            <td><b>CSS compression</b><br>Parses and removes redundant
                information:
                <ul>
                    <li>replaces multiple spaces with a single space</li>
                    <li>removes line-termination CR-LF characters</li>
                    <li>replaces tab characters with spaces</li>
                    <li>removes "/*" and "//" style comments</li>
                    <li>removes redundant spaces inserted in the 1<sup>st</sup>
                        step</li>
                    <li>removes spaces nearby a delimiter: :;{}</li>
                </ul>
            </td>
            <td>no optimization</td>
        </tr>
        <tr>
            <td>JS</td>
            <td>js</td>
            <td><b>JS compression</b><br> Parses and removes redundant
                information:
                <ul>
                    <li>replaces tab characters with spaces</li>
                    <li>replaces multiple spaces with a single space</li>
                    <li>removes line-termination CR-LF characters</li>
                    <li>removes "/*" and "//" style comments</li>
                    <li>removes redundant spaces inserted in the 1<sup>st</sup>
                        step</li>
                    <li>removes spaces nearby a delimiter:
                        .,:;=!+-*/&amp;|&lt;&gt;(){}"?</li>
                </ul>
            </td>
            <td>no optimization</td>
        </tr>
        <tr>
            <td>others</td><td>.*</td><td>not affected</td><td>not affected</td>
        </tr>
    </tbody>
</table>

## Examples

The following command line converts and optimizes `index.htm`, creates the output C-file `index.c`, and creates the
listing file `index.lst`:

```sh
fcarm index.htm
```

The following command line converts and optimizes a list of files, creates the output C-file `web.c`, and creates the
listing file `web.lst`:

```sh
fcarm index.htm, keil.gif, llblue.jpg, system.cgi TO web.c
```

The following command line converts and optimizes a list of files, creates the output C-file `web.c`, and suppresses the
creation of the listing file (`nopr` directive). The files are located in the sub-folder `Web_Files`:

```sh
fcarm index.htm, keil.gif, llblue.jpg, system.cgi TO web.c nopr root(Web_Files)
```

The following command line converts and optimizes a list of files, creates the output C-file `web.c`, and creates the
listing file `web.lst`. The file `doStuff.js` is excluded from optimization:

```sh
fcarm index.htm, keil.gif, llblue.jpg, system.cgi, ~doStuff.js TO web.c
```

The following command line uses a command file:

```sh
fcarm @fcarm_command_file
```

## Directives

### PRINT

The **PRINT** directive specifies the name of the listing file. If no PRINT directive is specified the listing file is given
the name of the generated  c-source file with a .LST extension.

- Abbreviation: PR
- Arguments: `PRINT (filename)`
- Default: The name of the generated listing file with a .LST extension.

See also: [NOPRINT](#noprint)

**Example**

```sh
fcarm index.htm, keil.gif to web.c print (Sample.lst)
```

### NOPRINT

The **NOPRINT** directive prevents the file converter from generating a listing file.

- Abbreviation: `NOPR`
- Arguments: `NOPRINT`
- Default: The name of the generated listing file with a .LST extension.

See also: [PRINT](#print)

**Example**

```sh
fcarm index.htm, keil.gif to web.c noprint
```

### PAGEWIDTH

The **PAGEWIDTH** directive specifies the number of character per line that may be printed to the converter listing file.
Lines with more than the specified number of characters are broken into two or more lines. The valid range of values is
72-132 columns.

- Abbreviation: `PW`
- Arguments: `PAGEWIDTH (number)`
- Default: PAGEWIDTH (132)

See also: [PAGELENGTH](#pagelength)

**Example**

```sh
fcarm index.htm to web.c pagewidth (132)
```

### PAGELENGTH

The **PAGELENGTH** directive specifies the number of lines printed per page in the converter listing file. The minimum page
length is 10 lines per page. The maximum page length is 65535.

- Abbreviation: `PL`
- Arguments: `PAGELENGTH (number)`
- Default: PAGELENGTH (60)

See also: [PAGEWIDTH](#pagewidth)

**Example**

```sh
fcarm index.htm to web.c pagelength (55)
```

### ROOT

The **ROOT** directive defines the root path where the web files are located relative to the project directory path.

- Abbreviation: `RO`
- Arguments: `ROOT (directory)`
- Default: The current project directory path is used as the web container.

**Example**

```sh
fcarm index.htm, keil.gif to web.c root(Web_Files)
```

[**Installation**](./01_installation.md) **&laquo; Chapters &raquo;** [**ElfDwt**](./03_elfdwt.md)