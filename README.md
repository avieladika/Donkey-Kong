# Donkey Kong — C++ Console Game

An academic Donkey Kong-inspired console game with file-based levels, enemies, recording, and replay modes.

## Highlights

- Game objects for Mario, barrels, ghosts, and the board.
- Multiple screen files and difficulty settings.
- Recorded input steps and random seeds for replay.
- Replay result checks for expected game events.
- C++ inheritance and polymorphism for game modes and enemy behavior.

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

## Project structure

`Game*` implements game modes, `Board` loads and represents levels, `Mario`/`Barrel`/`Ghost` implement game objects, and `Steps`/`Results` handle recordings and expected outcomes.

## Scope and credits

Academic game project. Donkey Kong and its characters belong to their respective owners; this repository is an educational implementation. The replay checker is not a general automated unit-test suite. Windows console APIs make portability an additional task.
