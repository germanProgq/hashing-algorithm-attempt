# hashing-algorithm-attempt

A personal experiment in designing a hashing algorithm from scratch in C++. It builds a large internal state (a 2048-bit "fortress" of 32 64-bit words), mixes input data into it, and adds a few extra ideas on top like self-healing state snapshots and an optional performance/mixing pass.

This is a learning project. It has not been analyzed or reviewed by cryptographers. Do not use it for passwords, signatures, integrity checks, or anything where a real hash function matters. Use an established, vetted algorithm for that.

## What is in here

- `QuantumProtection.*`: the core state (`QFState`) and the mixing routines. The name is the author's label for the design, not a claim about quantum resistance.
- `SelfHeal.*`: a ring buffer of state snapshots with per-word and whole-snapshot checksums, meant to detect and recover from corruption of the internal state.
- `UniversalData.*`: handling for feeding arbitrary input (files or strings) into the state.
- `Performance.*`: an optional pass that tries to speed up or re-mix the state using vector instructions.
- `main.cpp`: a small command-line driver.

## Build

The repo is a Visual Studio solution (`Hashing.sln`), targeting C++ on Windows with Debug and Release configurations for x86 and x64.

Open `Hashing.sln` in Visual Studio 2022 and build, or from a Developer Command Prompt:

```
msbuild Hashing.sln /p:Configuration=Release /p:Platform=x64
```

The files are plain C++17 and can also be compiled directly with any C++ compiler, for example:

```
g++ -std=c++17 -O2 Hashing/*.cpp -o hashing
```

## Run

```
hashing string "Hello, Universe!"
hashing file myBinary.dat
```

If the named file cannot be opened, the program falls back to asking for a string on standard input.

## License

MIT (see `LICENSE.txt`).
