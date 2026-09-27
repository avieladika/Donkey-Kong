# Donkey Kong — C++ Console Game

![C++](https://img.shields.io/badge/C%2B%2B-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Windows Console](https://img.shields.io/badge/Windows_Console-0078D6?style=for-the-badge)

**Links:** [Repository](https://github.com/avieladika/Donkey-Kong) · [Source](Code%20Files) · [Original instructions](Game_Instructions.rtf)

An academic Donkey Kong-inspired console game with file-based levels, multiple enemy behaviors, and modes for interactive play, recording, and replay.

## The Challenge

A console game must coordinate movement, collisions, enemies, and progression. Reproducing a game session adds another challenge: inputs, random behavior, and expected results need to be recorded consistently.

## The Solution

The project separates boards, game objects, and game modes into C++ classes. Recording stores input steps and random seeds, while replay uses saved data and can compare game events with expected outcomes.

## Highlights

### Recording and replay through simulation steps

Saved sessions record the difficulty, random seed, and input characters paired with iteration numbers. Replay reads those steps and initializes random generators from the stored seed. The result-checking mode compares recorded events, such as deaths and level completion, against the simulation's iteration count. This makes a session inspectable through its inputs and expected events; it is not a guarantee of identical behavior across every platform or compiler.

See [Steps](Code%20Files/Steps.cpp), [Results](Code%20Files/Results.cpp), and [replay checking](Code%20Files/GameSilent.cpp).

### State-based movement and collision rules

Mario, barrels, and ghosts update their positions according to board tiles, movement direction, ladders, jumping, and falling state. Ghost behavior includes probabilistic direction choices with C++ random-number facilities. These are rule-based movement algorithms; the project does not implement a general shortest-path planner such as A*.

### Polymorphic game objects and game modes

C++ inheritance separates regular and special ghost behavior and organizes interactive, recording, and replay modes. Ghost collections use `std::unique_ptr`, tying object lifetime to ownership in the collection. Level layouts are loaded from `.screen` files, allowing board data to remain separate from movement logic.

### Technologies and dependencies

| Component | How it is used |
| --- | --- |
| **C++ standard library** | Containers, strings, file streams, smart pointers, and random-number generation such as `std::mt19937`. |
| **Windows console API (`windows.h`)** | Console cursor positioning, visibility, and platform-specific presentation helpers. |
| **Microsoft console I/O (`conio.h`)** | Keyboard input facilities used by the Windows console application. |
| **Visual Studio / MSVC** | The included solution and project files configure the Windows C++ build. |
| **Text-based level and recording formats** | `.screen`, `.steps`, and `.result` files store boards, session inputs, and expected outcomes. |

The game uses standard-library and Windows platform facilities rather than a third-party game engine. Movement, collision rules, level handling, and replay logic are implemented in the project.


## What It Includes

- Level loading from `.screen` files.
- Mario, barrels, and multiple ghost behaviors.
- Interactive, save, load, and silent replay modes.
- Recorded input steps and random seeds.
- Result checking for recorded game events.
- Visual Studio solution for the Windows console.

## System Model

`Game*` classes implement game modes; `Board` represents levels; Mario, barrels, and ghosts implement game objects. `Steps` and `Results` store the information used for recording and replay.

## Core Technical Flow

Load level → initialize game objects → process input or replay steps → update collisions/state → record or compare events.

```mermaid
flowchart LR
    L[Level files] --> G[Game loop]
    I[Live input or saved steps] --> G
    G --> O[Game objects and collisions]
    O --> R[Recorded or checked results]
```

## Why This Design

Game-object classes organize distinct behaviors. Saved steps and outcomes provide a way to inspect repeatable sessions, although replay checking is not a substitute for unit tests.

## Build and run

The project targets the Windows console and includes a Visual Studio solution.

1. Install Visual Studio with the Desktop development with C++ workload.
2. Open `Code Files/Donkey_Kong_AN.sln` and build the application.
3. Set the working directory to `Code Files` so the `.screen`, `.steps`, and `.result` files can be found.
4. Launch the built executable. Use the menu for game instructions and difficulty.

Supported command-line arguments:

| Arguments | Mode |
| --- | --- |
| none | Interactive play |
| `-save` | Record a game |
| `-load` | Replay a recording |
| `-load -silent` | Replay with result checking |

Additional original instructions are in `Game_Instructions.rtf`.

## Scope and credits

Academic game project. Donkey Kong and its characters belong to their respective owners; this repository is an educational implementation. The replay checker is not a general automated unit-test suite. Windows console APIs make portability an additional task.
