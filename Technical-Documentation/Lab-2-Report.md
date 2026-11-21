
# Lab 2: C Libraries, Linking, and ELF Executable Structure

## 1. Introduction

This practical lab explores C libraries, static and dynamic linking, and the internal structure of ELF (Executable and Linkable Format) files in a Linux environment.

The practical uses a C program named `procinfo.c` to display process information and investigate how Linux handles executable files and library dependencies.

## 2. Objectives

- Understand C header files and their purpose.
- Identify static and shared libraries in Linux.
- Compile programs using static and dynamic linking.
- Compare executable file sizes.
- Examine ELF headers and program headers.
- Inspect dynamic library dependencies.

## 3. Environment and Tools

| Tool | Purpose |
|---|---|
| Ubuntu Linux | Practical environment |
| GCC | C compiler |
| Readelf | ELF file analysis |
| ldd | Library dependency inspection |
| Docker | Linux environment |
| C | Programming language |

## 4. Project Structure

```text
Lab-2-C-Libraries/
├── Screenshots/
├── Source-Code/
│   └── procinfo.c
├── Technical-Documentation/
│   └── Lab-2-Report.md
├── .gitignore
└── README.md
```

## 5. Source Code Analysis

The `procinfo.c` program uses the following header files:

- `stdio.h`: Provides input and output functions.
- `stdlib.h`: Provides general utility functions.
- `unistd.h`: Provides process-related functions.
- `time.h`: Provides date and time functions.

The program uses:
- `getpid()` to retrieve the current process ID.
- `getppid()` to retrieve the parent process ID.
- `time()` to obtain the current time.
- `localtime()` to convert time into local time.
- `asctime()` to display the formatted time.

## 6. Header Files and Libraries

Header files were investigated inside `/usr/include/`.

The `getpid()` declaration was located using:

```bash
grep "getpid" /usr/include/unistd.h | head -2
```

The following library files were identified:

```text
/lib/x86_64-linux-gnu/libc.so
/lib/x86_64-linux-gnu/libc.so.6
/usr/lib/x86_64-linux-gnu/libc.a
```

`libc.so.6` is a shared C library, while `libc.a` is a static C library archive.

## 7. Dynamic and Static Linking

### 7.1 Dynamic Linking

The dynamic executable was created using:

```bash
gcc procinfo.c -o procinfo_dynamic
```

Dynamic linking allows an executable to use shared libraries at runtime.

### 7.2 Static Linking

The static executable was created using:

```bash
gcc -static procinfo.c -o procinfo_static
```

Static linking includes the required library code within the executable.

### 7.3 Executable Size Comparison

| Executable | Observed Size |
|---|---:|
| procinfo_dynamic | 16 KB |
| procinfo_static | 922 KB |

The static executable was significantly larger because it includes required library code.

## 8. ELF Header Analysis

The ELF header was examined using:

```bash
readelf -h procinfo_dynamic
```

Important observations:

- Class: ELF64
- Data: 2's complement, little endian
- Type: DYN (Position-Independent Executable)
- Machine: Advanced Micro Devices X86-64
- Entry point address: 0x1140
- Number of program headers: 13
- Number of section headers: 31

These details identify the executable format, architecture, and important structural information.

## 9. Program Header Analysis

The program headers were inspected using:

```bash
readelf -l procinfo_dynamic
```

Program headers describe how different parts of an executable are arranged and loaded into memory.

Important entries may include:

- INTERP: Identifies the program interpreter.
- LOAD: Describes segments loaded into memory.
- DYNAMIC: Contains dynamic linking information.
- GNU_STACK: Describes stack-related permissions.

## 10. Dynamic Section Analysis

The dynamic section was examined using:

```bash
readelf -d procinfo_dynamic
```

The dynamic section contains information required by the dynamic linker, including shared library dependencies.

## 11. Library Dependency Analysis

Dependencies were inspected using:

```bash
ldd procinfo_dynamic
ldd procinfo_static
```

The dynamic executable uses shared library dependencies.

The static executable is expected to display:

```text
not a dynamic executable
```

This indicates that it does not rely on dynamic shared library loading in the same way as the dynamic executable.

## 12. Practical Testing

Both executables were tested using:

```bash
./procinfo_dynamic
./procinfo_static
```

The program was designed to display:

- Current Process ID (PID)
- Parent Process ID (PPID)
- Current Time
- Executable Path

## 13. Conclusion

This practical provided an understanding of C libraries, static and dynamic linking, and ELF executable structures in Linux.

The comparison showed that static executables are generally larger than dynamically linked executables because they contain the required library code.

ELF analysis commands such as `readelf` and `ldd` helped examine executable structure and library dependencies.

The practical improved understanding of how Linux compiles, links, and executes C programs.
