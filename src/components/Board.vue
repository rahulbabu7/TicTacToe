
<script setup>
import { ref,computed } from 'vue';

const player = ref("X");  //settting first player as X
const board = ref([
  ['','',''],
  ['','',''],
  ['','','']
])

//from react docs
// This function checks if there is a winner in a tic-tac-toe game.
const CalculateWinner = (squares) => {
  // These are the possible ways to win in tic-tac-toe. Each array represents a winning combination.
  const lines = [
    [0, 1, 2],  // Top row
    [3, 4, 5],  // Middle row
    [6, 7, 8],  // Bottom row
    [0, 3, 6],  // Left column
    [1, 4, 7],  // Middle column
    [2, 5, 8],  // Right column
    [0, 4, 8],  // Diagonal from top-left to bottom-right
    [2, 4, 6],  // Diagonal from top-right to bottom-left
  ];

  // Now, we're going to check each of these winning combinations.
  for (let i = 0; i < lines.length; i++) {
    // Get the three square positions (indices) we're going to check for a win.
    const [a, b, c] = lines[i];

    // Check if there's a symbol (either 'X' or 'O') in the first square of the current combination (squares[a]).
    // Then, see if the symbol in that square is the same as the symbols in the other two squares (squares[b] and squares[c]).
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      // If all three squares have the same symbol and it's not an empty square (null), we have a winner!
      // Return the symbol of the winner ('X' or 'O').
      return squares[a];
    }
  }

  // If we've checked all possible combinations and didn't find a winner, the game is not won yet.
  // So, we return null to indicate that there is no winner at this point.
  return null;
}

//calculating winner
const winner = computed(()=>CalculateWinner(board.value.flat()));

const makeMove = (x,y) =>{
  if(winner.value) return   //already found a winner
  if(board.value[x][y] !== '')return //the square box is not empty

  board.value[x][y] = player.value  //if its x turn the mark board with X
  //if its O turn the mark the board with O

  //changing the player turn
  player.value = player.value ==='X' ? 'O' : 'X';
  //if player is x then change it to O 
  //if player is O the change it to X


}

//Reseting the game 
const resetGame = ()=>{
   player.value = "X";  //settting first player as X
board.value = [
  ['','',''],
  ['','',''],
  ['','','']
]
}


</script>

<template>
<main class="pt-8 text-center dark:bg-gray-800 min-h-screen dark: text-white ">
  <h1 class="mb-8 text-3xl font-bold uppercase">
   Tic Tac Toe 
  </h1>

  <h3 class="text-xl mb-4">Player {{ player }}'s turn</h3>
<!-- 

  Let's break this down step-by-step:

1. The outer <div> renders a column flex container to center the content. 

2. The v-for loop iterates through each row in the 'board' data variable. 

3. It outputs a <div> for each row, using x as the key. The row <div> is a flex container.

4. Inside each row, another v-for loops through each cell in that row array. 

5. It outputs a <div> for each cell, using y as the key.

6. The @click handler calls the makeMove() method when a cell is clicked, passing the x,y indexes.

7. The :class binding dynamically assigns CSS classes to each cell <div> based on:

   - Default styles for all cells  
   - Added .text-pink-500 or .text-blue-500 class based on cell's value
   - So X cells get pink text, O cells get blue text

8. The template expression displays 'X', 'O', or blank for each cell based on its value.

So in summary, we:

- Loop through each row 
- Inside that, loop through each cell
- Output a <div> for each cell
- Assign click handler and conditional styling
- Display X, O or blank for each cell

This allows us to generate the typical TicTacToe board dynamically in Vue. Let me know if any part is unclear! -->
  <div class="flex flex-col items-center mb-8">

    <div
     v-for="(row,x) in board"
     :key="x"
     class="flex"
    >
    <div
     v-for="(cell,y) in row"
     :key="y"
     @click="makeMove(x,y)"
     :class="`border border-white w-20 h-20 hover:bg-gray-700 flex
     items-center justify-center material-icons-outlined text-4xl cursor-pointer ${ cell ==='X'? 'text-pink-500' :'text-blue-500'}`"
    >
    {{ cell ==='X'?'X':cell ==='O' ?'O' :' ' }}
    
    </div>
    </div>
  </div>
<h2 class="text-6xl font-bold mb-8" v-if="winner">
  Player "{{ winner }}" Wins
</h2>
<button @click="resetGame" class="px-4 py-2 bg-pink-500 rounded uppercase font-bold hover:bg-pink-600 duration-300"> reset game</button>
</main>

</template>
