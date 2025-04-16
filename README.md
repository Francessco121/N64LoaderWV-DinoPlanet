# N64 ROM Loader for Ghidra by Warranty Voider

this is a loader module for ghidra for the Dinosaur Planet ROM
- fixes endianess (little, big, mixed) at loading
- loads ram, rom and boot section into ghidra
- it can use a signature/pattern file to scan for symbol hints for ghidra

Dinosaur Planet specific functionality
- resolves DLL import tables so that DLL-local code is properly referencing function addresses, strings, and other constants
- initializes each DLL function named after their DLL, as well as object name if any
- sets up GP register for each DLL so it can read stuff. the game patches its own assembly for this at runtime
- attempts to make decent-ish references for global DLLs using a fake redirection table in-place of the runtime DLL table - however results may vary
- also note this is the first thing i wrote in java (and hopefully the last) so apologies for inconsistencies in naming conventions etc.

this allows a rom to be labeled, disassembled and decompiled

credits:
- [blackgamma7](https://github.com/blackgamma7) for fixing memory layout stuff, adding register symbols and various small changes [see merge commit](https://github.com/zeroKilo/N64LoaderWV/commit/46137048775a41f4b54c08cf3c3fab1bcb962219)
- [dmattia](https://github.com/dmattia) for adding build instructions for mac

requires JDK 17

[![Alt text](https://img.youtube.com/vi/3d3a39LuCwc/0.jpg)](https://www.youtube.com/watch?v=3d3a39LuCwc)

[![Alt text](https://img.youtube.com/vi/fhI3Vpw7FVk/0.jpg)](https://www.youtube.com/watch?v=fhI3Vpw7FVk)

## Build from Source (Mac)

```bash
brew install java
brew install gradle
brew cask install ghidra

export GHIDRA_INSTALL_DIR=`brew cask ls ghidra | grep ghidra | sed 's/^.*-> \(.*\)ghidraRun.*/\1/'`
```

Then whenever you're ready to build, run

```bash
gradle
```

and it will create a zip file in `/dist` that you can use that file as the extension in Ghidra
