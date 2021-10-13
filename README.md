# chess.js
chess.js is a Javascript chess library that is used for chess move generation/validation, piece placement/movement, and check/checkmate/stalemate detection - basically everything but the AI.
# Example Code
The code below plays a random game of chess:

const { Chess } = require('./chess.js')
const chess = new Chess()

while (!chess.game_over()) {
    const moves = chess.moves()
    const move = moves[Math.floor(Math.random() * moves.length)]
    chess.move(move)
}
console.log(chess.pgn())
