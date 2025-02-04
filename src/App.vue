<script setup lang="ts">
import { ref, onMounted } from 'vue';
import gsap from 'gsap';

const showMessage = ref(false);
const showButtons = ref(false);
const introText = ref('');
const messages = [
  'Hallo Sophie ...',
  'Ich hab da eine ganz ganz wichtige Frage für dich ...',
  'Willst du mein Valentin sein? 💖'
];
let messageIndex = 0;

const displayNextMessage = () => {
  if (messageIndex < messages.length) {
    introText.value = messages[messageIndex];
    messageIndex++;
    setTimeout(displayNextMessage, 4000);
  } else {
    showButtons.value = true;
  }
};

const sayYes = () => {
  showMessage.value = true;
  showButtons.value = false;
  gsap.fromTo(
    '#love-message',
    { scale: 0, opacity: 0 },
    { scale: 1, opacity: 1, duration: 1, ease: 'bounce.out' }
  );
};

const moveNo = () => {
  gsap.to('#no-btn', {
    x: Math.random() * 290 - 20,
    y: Math.random() * 290 - 20,
    duration: 0.1
  });
};

onMounted(() => {
  displayNextMessage();
});
</script>

<template>
  <div class="valentine-container">
    <h2>{{ introText }}</h2>
    <video
      id="panda"
      src="https://i.imgur.com/Qhprx77.mp4"
      class="panda"
      autoplay
      loop
      muted
    />
    <div v-if="showButtons" class="buttons">
      <button @click="sayYes" class="yes-btn">Ja! 💘</button>
      <button @mouseover="moveNo" id="no-btn" class="no-btn">Nein 😢</button>
    </div>
    <p v-if="showMessage" id="love-message" class="message">
      🥹 Ich LIEBE dich! 🐼💕
    </p>
  </div>
</template>

<style scoped>
:root {
  --barbie-pink: #e0218a;
}

.valentine-container {
  text-align: center;
  font-family: 'Arial', sans-serif;
  padding: 20px;
  margin: 0 auto;
  max-width: 400px;
}

.panda {
  width: 100%;
  max-width: 300px;
  margin: 20px 0;
  border-radius: 15px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.yes-btn,
.no-btn {
  font-size: 1.2em;
  padding: 12px 24px;
  border: none;
  cursor: pointer;
  border-radius: 25px;
  transition: all 0.3s ease;
  min-width: 120px;
}

.yes-btn {
  background-color: var(--barbie-pink);
  color: white;
  box-shadow: 0 4px 14px rgba(224, 33, 138, 0.4);
}

.yes-btn:hover,
.yes-btn:focus {
  background-color: #c81c75;
  box-shadow: 0 6px 16px rgba(224, 33, 138, 0.6);
  transform: translateY(-2px);
}

.no-btn {
  background-color: #f0f0f0;
  color: #333;
  position: relative;
}

.no-btn:hover,
.no-btn:focus {
  background-color: #e0e0e0;
  transform: translateY(-2px);
}

.message {
  font-size: 1.5em;
  color: var(--barbie-pink);
  margin-top: 20px;
}
</style>
