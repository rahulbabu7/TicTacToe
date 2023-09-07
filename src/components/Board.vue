<template>
   <main class="flex justify-center items-center h-screen">
    <section>
      Game
    </section>
   </main>
</template>

<script setup>
import { ref,computed } from 'vue';

const player = ref("X");
const board = ref([
  ['','',''],
  ['','',''],
  ['','','']
])

//from react docs
const CalculateWinner = (squares) =>{
  const lines = [
    //winning lines
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6]
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}


</script>