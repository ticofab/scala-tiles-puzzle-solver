Scala Tiles Puzzle Solver
=========================

This program solves the puzzle described by the image below.


# The Puzzle Rules

![puzzle](http://famsterdamworld.com/ticofab/puzzle.jpg)


# The Model

## Tiles

Each tile can be represented with a tuple of directions. The four directions are denoted with *N, E, W, S* with the shorthand of the four cardinal directions. If a tile is a beginning (no input connection) or an ending (no output connection) then it is denoted with *O*.

## Tile Relationships

We define the matching operator between the ends of two tiles with the ```=!=``` notation. An output ending can be connected with the counter direction of the input ending of the other tile. E.g. *N* with *S*, *W* with *E* and vice versa. The *O* "ending" cannot be connected with any other tile.

# The Solver

The solver uses recursive backtracking. We maintain the list of unused tiles, and we maintain a path. The returning list of the solver method is a list of complete paths, which have proper starting and ending tiles.

The solver filters those tiles in the input list which are prependable to the current path. For each prependable candidate, we call the solver recursively so that the selected tile is prepended to the path and removed form the list of unused tiles.

A solution is generated and appended to the list of returning paths if the selected tile is a beginning tile.

# Tricks

- we used implicit class to wrap the ```isPrependable()``` method around the ```Path``` type
- we used *combinators* (```filter()```, ```flatMap()```, etc.) to implement the solver's algorithm
- the only ugly thing is the body of the ```flatMap()```
  - where removing a given item from a list is not simple - technically you have to reconstruct the list with ```drop()``` and ```tail()```,
  - also, the optional appending to the returning value is not elegant

You are welcome to give your suggestions about how to eliminate these "uglinesses". :-)
