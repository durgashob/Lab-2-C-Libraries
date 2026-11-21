
# Lab 2: C Libraries, Linking, and ELF Executable Structure

## Overview
This lab explores C libraries, static and dynamic linking, and the internal structure of ELF executables in a Linux environment.

## Objectives
- Understand C header files and libraries.
- Identify static and shared library files.
- Compile programs using static and dynamic linking.
- Examine ELF executable headers and program headers.
- Analyze dynamic dependencies using `ldd`.

## Technologies and Tools
- Ubuntu Linux
- GCC Compiler
- GNU Readelf
- Linux `ldd` Command
- C Programming Language
- Docker

## Project Structure
```text
Lab-2-C-Libraries/
├── Screenshots/
├── Source-Code/
│   └── procinfo.c
├── Technical-Documentation/
├── .gitignore
└── README.md
```

## Compilation Commands

### Dynamic Linking
```bash
gcc procinfo.c -o procinfo_dynamic
```

### Static Linking
```bash
gcc -static procinfo.c -o procinfo_static
```

## ELF Analysis Commands
```bash
file procinfo_dynamic
readelf -h procinfo_dynamic
readelf -l procinfo_dynamic
readelf -d procinfo_dynamic
ldd procinfo_dynamic
ldd procinfo_static
```

## Key Findings
- The dynamic executable was approximately 16 KB.
- The static executable was approximately 922 KB.
- The dynamic executable uses shared library dependencies.
- The static executable includes required library code.

## Author
Durga Shob
