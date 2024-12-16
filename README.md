# libmpv latest build

This repo provides already built `.lib` files. The `.libs` are obtained the following way:

### Downloading the Build

- *Source*: Download the latest `libmpv` builds from [SourceForge](https://sourceforge.net/projects/mpv-player-windows/files/libmpv/)

### Generating the Import Library (`.lib`)

Since `libmpv` does not come with pre-built `.lib` file, you need to generate it using Visual Studio tools. Follow these steps:

1. **Open Visual Studio Developer Command Prompt**
    - Provides access to `dumpbin` and `lib.exe`

2. **Generate the Module Definition File** (`.def`)
```cmd
dumpbin /exports libmpv-2.dll > libmpv.def
```

3. **Clean Up the `.def` File**
    - Open `libmpv.def` in a text editor
    - Remove unnecessary lines, leaving only the EXPORTS keyword and the list of exported function names.


4. **Create the Import Library**

- For 64-bit systems:
    ```cmd
    lib.exe /def:libmpv.def /machine:x64 /out:mpv.lib
    ```

- For 32-bit systems:
    ```cmd
    lib.exe /def:libmpv.def /machine:x86 /out:mpv.lib
    ```
**Note:** Generating the `.lib` file this way works, but preferably you should build from [source](https://github.com/mpv-player/mpv).