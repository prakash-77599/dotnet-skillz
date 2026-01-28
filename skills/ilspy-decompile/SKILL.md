---
name: ilspy-decompile
description: Decompiles .NET assemblies to C# source code using ILSpy. Use when the user needs to decompile DLLs, view decompiled source code, list types in assemblies, or generate projects from compiled .NET binaries.
allowed-tools: Bash(dnx:*)
---

# .NET Assembly Decompilation with ILSpy

## Quick start

```bash
# Decompile an assembly to stdout (no install needed with .NET 10+)
dnx ilspycmd MyLibrary.dll

# Decompile to an output folder
dnx ilspycmd -o output-folder MyLibrary.dll
```

## Core workflow

1. Identify the assembly to decompile
2. Choose output format (C#, IL, or project)
3. Run dnx ilspycmd with appropriate options
4. Review decompiled source code

## Commands

### Basic Decompilation

```bash
# Decompile to stdout
dnx ilspycmd MyLibrary.dll

# Decompile to output directory
dnx ilspycmd -o ./decompiled MyLibrary.dll

# Decompile as compilable project
dnx ilspycmd -p -o ./project MyLibrary.dll

# Decompile with nested namespace folders
dnx ilspycmd -p -o ./project --nested-directories MyLibrary.dll
```

### Targeted Decompilation

```bash
# Decompile a specific type
dnx ilspycmd -t Namespace.ClassName MyLibrary.dll

# Decompile with specific C# version
dnx ilspycmd -lv CSharp11_0 MyLibrary.dll

# Decompile with reference path for dependencies
dnx ilspycmd -r ./dependencies MyLibrary.dll
```

### View IL Code

```bash
# Show IL code instead of C#
dnx ilspycmd -il MyLibrary.dll

# Show IL for specific type
dnx ilspycmd -il -t Namespace.ClassName MyLibrary.dll
```

### List Types

```bash
# List all classes
dnx ilspycmd -l class MyLibrary.dll

# List interfaces
dnx ilspycmd -l interface MyLibrary.dll

# List structs
dnx ilspycmd -l struct MyLibrary.dll

# List enums
dnx ilspycmd -l enum MyLibrary.dll

# List delegates
dnx ilspycmd -l delegate MyLibrary.dll
```

### Generate PDB

```bash
# Generate PDB for debugging
dnx ilspycmd -genpdb MyLibrary.dll
```

### Options

```bash
# Show version
dnx ilspycmd -v

# Show help
dnx ilspycmd -h

# Disable update check (useful for CI/automation)
dnx ilspycmd --disable-updatecheck MyLibrary.dll

# Remove dead code
dnx ilspycmd --no-dead-code MyLibrary.dll
```

## Example: Decompile NuGet package DLL

```bash
# Find and decompile a package DLL
dnx ilspycmd ~/.nuget/packages/newtonsoft.json/13.0.1/lib/netstandard2.0/Newtonsoft.Json.dll

# Decompile to project for analysis
dnx ilspycmd -p -o ./newtonsoft-src ~/.nuget/packages/newtonsoft.json/13.0.1/lib/netstandard2.0/Newtonsoft.Json.dll
```

## Example: Inspect specific type

```bash
# List all classes first
dnx ilspycmd -l class MyLibrary.dll

# Then decompile the specific type you need
dnx ilspycmd -t MyNamespace.MyClass MyLibrary.dll
```

## Example: Compare C# and IL

```bash
# View C# source
dnx ilspycmd -t MyNamespace.MyClass MyLibrary.dll

# View IL code for same type
dnx ilspycmd -il -t MyNamespace.MyClass MyLibrary.dll
```

## C# Language Versions

Available versions for `-lv` option:
- CSharp1, CSharp2, CSharp3, CSharp4, CSharp5, CSharp6, CSharp7, CSharp7_1, CSharp7_2, CSharp7_3
- CSharp8_0, CSharp9_0, CSharp10_0, CSharp11_0, CSharp12_0
- Latest, Preview
