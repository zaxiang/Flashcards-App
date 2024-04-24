<template>
  <div class="mx-3 my-3">

    <b-jumbotron v-if="currentFlashcard" class="flashcard">
      <h1 class="problem-text">{{ currentFlashcard.problem }}</h1>
      <b-button-group vertical>
        <b-button
          v-for="(choice, index) in currentFlashcard.choices"
          :key="index"
          @click="checkAnswer(index)"
          variant="primary"
          class="choice-button"
        >
        {{ index + 1 }}. {{ choice }}
        </b-button>
      </b-button-group>
    </b-jumbotron>
    <!-- <div v-if="isCorrect !== null">
      <b-alert :variant="isCorrect ? 'success' : 'danger'" dismissible @dismiss="resetResult">
        {{ isCorrect ? 'Correct!' : 'Incorrect. Try again.' }}
      </b-alert>
    </div> -->
    <!-- <div v-else>
      <p>Congratulations! You've completed all flashcards.</p>
    </div> -->

    <!-- <div class="flashcard">
      <span class="flashcard-content">Orange Flashcard</span>
    </div> -->

  </div>
</template>

<script setup lang="ts">
import flashcards from '../public/flashcards.json';
import { ref } from "vue"

let currentIndex = 0;

const currentFlashcard = ref(flashcards[currentIndex]);

function checkAnswer(selectedIndex: number) {
  if (selectedIndex === currentFlashcard.value.correctChoiceIndex) {
    alert('Correct!');
  } else {
    alert('Incorrect.');
  }

  // Move to the next flashcard
  currentIndex++;
  if (currentIndex < flashcards.length) {
    currentFlashcard.value = flashcards[currentIndex];
  } else {
    // Reset to the first flashcard if we reach the end
    currentIndex = 0;
    currentFlashcard.value = flashcards[currentIndex];
  }
}

</script>

<style scoped>
.flashcard {
  background-color: orange;
  padding: 120px;
  border-radius: 8px;
  display: inline-block;
}


.choice-button {
  background-color: #dbd334; /* Change this color as desired */
  color: white;
  margin-bottom: 18px;
  font-weight: bold;
  font-size: 18px; 
  padding: 10px;
}

.problem-text {
  color: white;
}
</style>
