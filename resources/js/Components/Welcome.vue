<template>
  <div class="containerMain">
    <h1>Welcome to Lucas Poker Odds Calculator!</h1>
    <div class="pokerhandsDisplay">
      <!-- Player inputs -->
      <input v-model="player1Hand" placeholder="Player 1 Hand (e.g., Qs Ks)" readonly/>
      <input v-model="player2Hand" placeholder="Player 2 Hand (e.g., Qd Kd)" readonly/>
      <input v-model="boardCards" placeholder="Board Cards (e.g., Js Ts 5h Td)" readonly/>
      
      <!-- Buttons to calculate odds and clear inputs -->
      <button @click="calculateOdds">Calculate Odds</button>
      <button @click="clearAllInputs">Clear All</button>
      
      <!-- Display results -->
      <div v-if="results">
        {{ results }}
      </div>
    </div>
    <div class="pokerCards">
      <!-- Display card images -->
      <div 
        v-for="(image, card) in cardImages" 
        :key="card" 
        class="card" 
        :class="{ selected: isCardSelected(card) }"
        @click="addCard(card)"
      >
        <img :src="image" :alt="card" class="card-image"/>
        <div class="card-label">{{ formatCardLabel(card) }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { TexasHoldem } from 'poker-odds-calc';
import './Welcome.css';
import { cardImages } from '@/cardImages'; // Adjust path if necessary

export default {
  name: 'Welcome',
  data() {
    return {
      player1Hand: '',
      player2Hand: '',
      boardCards: '',
      results: null,
      cardImages, // Imported card images mapping
      selectedPlayer1Cards: [],
      selectedPlayer2Cards: [],
      selectedBoardCards: [],
    };
  },
  methods: {
    addCard(card) {
      // Check which input is active and add card accordingly
      if (this.selectedPlayer1Cards.length < 2) {
        this.selectedPlayer1Cards.push(card);
        this.player1Hand = this.selectedPlayer1Cards.join(' ');
      } else if (this.selectedPlayer2Cards.length < 2) {
        this.selectedPlayer2Cards.push(card);
        this.player2Hand = this.selectedPlayer2Cards.join(' ');
      } else if (this.selectedBoardCards.length < 5) {
        this.selectedBoardCards.push(card);
        this.boardCards = this.selectedBoardCards.join(' ');
      } else {
        alert('All hands and board are full.');
      }
    },
    formatCardLabel(card) {
  // The last character of the card string represents the suit
  const suit = card.slice(-1);
  // The rest of the card string represents the rank
  const rank = card.slice(0, -1);

  // Map suits and ranks to their full names
  const suitMap = {
    'c': 'Clubs',
    'd': 'Diamonds',
    'h': 'Hearts',
    's': 'Spades',
  };
  const rankMap = {
    '2': '2',
    '3': '3',
    '4': '4',
    '5': '5',
    '6': '6',
    '7': '7',
    '8': '8',
    '9': '9',
    'T': '10',
    'J': 'Jack',
    'Q': 'Queen',
    'K': 'King',
    'A': 'Ace',
  };

  // Format and return the card label
  return `${rankMap[rank] || rank} of ${suitMap[suit]}`;
}
,
    calculateOdds() {
      const Table = new TexasHoldem();

      // Parse input fields into card arrays
      const player1Cards = this.player1Hand.trim().split(/\s+/); // Example: ["Qs", "Ks"]
      const player2Cards = this.player2Hand.trim().split(/\s+/); // Example: ["Qd", "Kd"]
      const boardCardsArray = this.boardCards.trim().split(/\s+/); // Example: ["Js", "Ts", "5h", "Td"]

      // Add players and board cards to the table
      Table
        .addPlayer(player1Cards)
        .addPlayer(player2Cards)
        .setBoard(boardCardsArray);

      // Calculate results
      const Result = Table.calculate();

      // Format results
      const formattedResults = Result.getPlayers().map((player, index) => {
        return `Player #${index + 1} - ${player.getHand()} - Wins: ${player.getWinsPercentageString()} - Ties: ${player.getTiesPercentageString()}`;
      }).join('\n');

      // Set results
      this.results = formattedResults;

      // Optionally, log additional details
      console.log("Player one hand " + player1Cards);
      console.log("Player two hand " + player2Cards);
      console.log(`Board: ${Result.getBoard()}`);
      console.log(`Iterations: ${Result.getIterations()}`);
      console.log(`Time takes: ${Result.getTime()}ms`);
    },
    clearAllInputs() {
      // Reset input fields and card selections
      this.player1Hand = '';
      this.player2Hand = '';
      this.boardCards = '';
      this.results = null;
      this.selectedPlayer1Cards = [];
      this.selectedPlayer2Cards = [];
      this.selectedBoardCards = [];
    },
    isCardSelected(card) {
      return this.selectedPlayer1Cards.includes(card) ||
             this.selectedPlayer2Cards.includes(card) ||
             this.selectedBoardCards.includes(card);
    }
  }
};
</script>