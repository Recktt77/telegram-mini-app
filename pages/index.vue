<script setup lang="ts">
import { ref } from 'vue';

// Placeholder for user information
const userName = ref("User");

// PDD test questions
const questions = ref([
  {
    question: "Какой знак запрещает движение?",
    options: ["Стоп", "Въезд запрещен", "Ограничение скорости"],
    correctAnswer: 1,
  },
  {
    question: "Какой сигнал светофора означает движение?",
    options: ["Красный", "Желтый", "Зеленый"],
    correctAnswer: 2,
  },
  // Добавьте больше вопросов по ПДД
]);

const currentQuestion = ref(0);
const userAnswer = ref<number | null>(null);
const score = ref(0);
const gameStarted = ref(false);

// Обработка ответа пользователя в тесте
function handleAnswer(optionIndex: number) {
  userAnswer.value = optionIndex;

  if (optionIndex === questions.value[currentQuestion.value].correctAnswer) {
    score.value++;
    alert("Правильно!");
  } else {
    alert("Неправильно! Попробуйте снова.");
  }

  if (currentQuestion.value < questions.value.length - 1) {
    currentQuestion.value++;
    userAnswer.value = null;
  } else {
    alert(`Тест завершен! Вы набрали ${score.value} очков.`);
    currentQuestion.value = 0;
    score.value = 0;
  }
}

// Открытие теста ПДД
function openTest() {
  alert("Открытие теста ПДД...");
  // Здесь вы можете отобразить вопросы теста (пока это только пример)
}

// Запуск мини-игры (игра в машину)
function startCarGame() {
  gameStarted.value = true;
  alert("Игра началась! Избегайте препятствий!");
}

// Состояние мини-игры
function stopCarGame() {
  alert("Игра завершена!");
  gameStarted.value = false;
}
</script>

<template>
  <section class="app-container">
    <h1>Pocket Driver</h1>
    <h2>Welcome, {{ userName }}!</h2>
    
    <div class="button-container">
      <button class="action-button" @click="openTest">Open PDD Test</button>
      <button class="action-button" @click="startCarGame">Earn Coins (Car Game)</button>
    </div>

    <nav class="nav-bar">
      <button class="nav-button">Home</button>
      <button class="nav-button">Profile</button>
      <button class="nav-button">Settings</button>
    </nav>

    <!-- PDD Test Section -->
    <div v-if="userAnswer !== null && currentQuestion < questions.length" class="test-section">
      <h2>{{ questions[currentQuestion].question }}</h2>
      <ul>
        <li v-for="(option, index) in questions[currentQuestion].options" :key="index">
          <button class="action-button" @click="handleAnswer(index)">
            {{ option }}
          </button>
        </li>
      </ul>
      <p>Текущий счет: {{ score }}</p>
    </div>

    <!-- Mini Car Game Section -->
    <div v-if="gameStarted" class="game-section">
      <h2>Car Game - Avoid the Obstacles!</h2>
      <p>Controls: Use arrow keys to move the car.</p>
      <button @click="stopCarGame">Stop Game</button>
      <!-- Здесь будет логика для мини-игры -->
    </div>
  </section>
</template>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #e0f7fa; /* Light blue background */
  color: #333;
}

h1 {
  color: #007bbd; /* Dark blue for the title */
}

h2 {
  color: #005f8c; /* Slightly darker blue for the welcome message */
}

.button-container {
  margin: 20px 0;
}

.action-button {
  background-color: #007bbd; /* Blue button color */
  color: white;
  border: none;
  padding: 15px 30px;
  border-radius: 5px;
  cursor: pointer;
  margin: 10px;
  font-size: 16px;
  transition: background-color 0.3s;
}

.action-button:hover {
  background-color: #005f8c; /* Darker blue on hover */
}

.nav-bar {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: #007bbd; /* Blue background for the nav bar */
  display: flex;
  justify-content: space-around;
  padding: 10px 0;
}

.nav-button {
  background-color: transparent;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
  transition: color 0.3s;
}

.nav-button:hover {
  color: #e0f7fa; /* Light blue on hover */
}

.test-section, .game-section {
  margin: 20px;
  text-align: center;
}
</style>
