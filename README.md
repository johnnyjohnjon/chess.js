# chess.js
chess.js is a Javascript chess library that is used for chess move generation/validation, piece placement/movement, and check/checkmate/stalemate detection - basically everything but the AI.

# Example Code
The code below plays a random game of chess:

 ``` 
const { Chess } = require('./chess.js')
const chess = new Chess()

while (!chess.game_over()) {
    const moves = chess.moves()
    const move = moves[Math.floor(Math.random() * moves.length)]
    chess.move(move)
}
console.log(chess.pgn()) 
```
# API 
The Chess() constructor takes an optional parameter which specifies the board configuration in Forsyth-Edwards Notation.
```
// board defaults to the starting position when called with no parameters
const chess = new Chess()

// pass in a FEN string to load a particular position
const chess = new Chess(
    'r1k4r/p2nb1p1/2b4p/1p1n1p2/2PP4/3Q1NB1/1P3PPP/R5K1 b - c3 0 19'
)
```
