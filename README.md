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
# .ascii()
Returns a string containing an ASCII diagram of the current position.

```
const chess = new Chess()

// make some moves
chess.move('e4')
chess.move('e5')
chess.move('f4')

chess.ascii()
// -> '   +------------------------+
//      8 | r  n  b  q  k  b  n  r |
//      7 | p  p  p  p  .  p  p  p |
//      6 | .  .  .  .  .  .  .  . |
//      5 | .  .  .  .  p  .  .  . |
//      4 | .  .  .  .  P  P  .  . |
//      3 | .  .  .  .  .  .  .  . |
//      2 | P  P  P  P  .  .  P  P |
//      1 | R  N  B  Q  K  B  N  R |
//        +------------------------+
//          a  b  c  d  e  f  g  h'
```

# .board()
Returns an 2D array representation of the current position. Empty squares are represented by null.
```
const chess = new Chess()

chess.board()
// -> [[{type: 'r', color: 'b'},
        {type: 'n', color: 'b'},
        {type: 'b', color: 'b'},
        {type: 'q', color: 'b'},
        {type: 'k', color: 'b'},
        {type: 'b', color: 'b'},
        {type: 'n', color: 'b'},
        {type: 'r', color: 'b'}],
        [...],
        [...],
        [...],
        [...],
        [...],
        [{type: 'r', color: 'w'},
         {type: 'n', color: 'w'},
         {type: 'b', color: 'w'},
         {type: 'q', color: 'w'},
         {type: 'k', color: 'w'},
         {type: 'b', color: 'w'},
         {type: 'n', color: 'w'},
         {type: 'r', color: 'w'}]]
```
# .clear()
Clears the board.
```
chess.clear()
chess.fen()
// -> '8/8/8/8/8/8/8/8 w - - 0 1' <- empty board
``` 
# .game_over()
Returns true if the game has ended via checkmate, stalemate, draw, threefold repetition, or insufficient material. Otherwise, returns false.
```
const chess = new Chess()
chess.game_over()
// -> false

// stalemate
chess.load('4k3/4P3/4K3/8/8/8/8/8 b - - 0 78')
chess.game_over()
// -> true

// checkmate
chess.load('rnb1kbnr/pppp1ppp/8/4p3/5PPq/8/PPPPP2P/RNBQKBNR w KQkq - 1 3')
chess.game_over()
// -> true
```
# .get(square)
Returns the piece on the square:
```
chess.clear()
chess.put({ type: chess.PAWN, color: chess.BLACK }, 'a5') // put a black pawn on a5

chess.get('a5')
// -> { type: 'p', color: 'b' },
chess.get('a6')
// -> null
```

# .in_checkmate()
Returns true or false if the side to move has been checkmated.
```
const chess = new Chess(
    'rnb1kbnr/pppp1ppp/8/4p3/5PPq/8/PPPPP2P/RNBQKBNR w KQkq - 1 3'
)
chess.in_checkmate()
// -> true
```
# .in_draw()
Returns true or false if the game is drawn (50-move rule or insufficient material).
```
const chess = new Chess('4k3/4P3/4K3/8/8/8/8/8 b - - 0 78')
chess.in_draw()
// -> true
```
