# What is this?
This is a meta package that contains links and general documentation
of a series packages intended to support the development of general purpose chess engines and tools.

1) [chess-core](https://github.com/leonkacowicz/chess-core):
   This package implements the foundational code that implements the basic chess abstractions. 
   It also implements a fast move generation function using techniques like magic-bitboards, 
   zobrist hashing and also fen encoding/decoding.
2) [chess-arbiter](https://github.com/leonkacowicz/chess-arbiter):
   This package implements a chess-arbiter: an executable that executes 2 UCI-compatible chess  
   engines (treated as black boxes) and makes them play against each other. It's useful to 
   assess the rating of one chess-engine against another. 
3) [chess-uci](https://github.com/leonkacowicz/chess-uci):
   This package implements a library for communicating between a chess front-end/arbiter
   and a chess-engine using the [UCI protocol](https://chessprogramming.org/UCI).
4) [chess-random-engine](https://github.com/leonkacowicz/chess-random-engine):
   This package implements a compatible _Random Engine_, which
   plays according to the following strategy: Every time it is asked to
   play a move in a given position it generates the list of legal moves
   and pick a random move from the list.
5) [chess-engine-diluter](https://github.com/leonkacowicz/chess-engine-diluter):
   This package implements an engine-wrapping diluter. It works by receiving another engine's
   executable path (let's call this the underlying engine) and a probability parameter _p_.
   Everytime the engine is requested to play a move in a given position,
   it will randomly choose between forwarding the request to the underlying engine, and picking
   a random move (like the chess-random-engine).
6) [chess-engine](https://github.com/leonkacowicz/chess-engine):
   This package implements a basic minimax-tree-searching chess engine. This
   implementation follows most of the techniques taught and explained in
   https://www.chessprogramming.org/. This engine uses a static evaluation function
   and serves as the basis for the chess-neuralnet-engine (details below).
7) [chess-neuralnet](https://github.com/leonkacowicz/chess-neuralnet):
   This package implements the two different neural network mechanisms to serve as a position 
   evaluation function to be used by minimax-tree-searching chess engines.
   The first is a simple MLP (multilayer perceptron), which can be trained using a variety of 
   algorithms. The second is [NEAT (Neuro Evolution of Augmenting Topologies)](
   https://nn.cs.utexas.edu/downloads/papers/stanley.ec02.pdf).
8) [chess-neuralnet-engine](https://github.com/leonkacowicz/chess-neuralnet-engine):
    This package is based on the `chess-engine` (mentioned above), and extends it by experimentally using
    neuralnets as position evaluation function at the leave nodes of the [minimax-tree](
    https://www.chessprogramming.org/Search_Tree).
9) [chess-neuralnet-engine-optimizer](https://github.com/leonkacowicz/chess-neuralnet-engine-optimizer):
    This package implements tools to train neuralnets used by chess-neuralnet-engine using self-play.
    Currently, it uses the iterated amplification-distillation algorithm.

# How do I build it?

All packages use CMake as a build-tool. In theory, they require CMake 3.5,
but I haven't tested it with previous versions of CMake. If you manage to
build it with an older version of CMake, let me know or send a pull request
decreasing the required version on line 1 of `/CMakeLists.txt`

To build each package:
```sh
mkdir build
cd build
cmake ..
make
```

# Testing
All tests implemented in each package are located in the `test/` directory. Each package
contain a main function that invoke all the tests and a CMake target that creates an executable
with this main function.