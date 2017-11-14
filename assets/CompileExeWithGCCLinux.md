[From Stackoverflow](https://stackoverflow.com/a/38788588/6765082)

Linux Subsystem works as a Linux-computer. You can only run Linux executables inside it and default gcc creates Linux executables.

To create Windows executables, you need to install mingw cross-compiler:

```sudo apt-get install mingw-w64```

Then you can create 32-bit Windows executable with:

```i686-w64-mingw32-gcc -o main32.exe main.c```

And 64-bit Windows executable with:

```x86_64-w64-mingw32-gcc -o main64.exe main.c```

Note that these Windows executables will not work inside Linux Subsystem, only outside of it.
