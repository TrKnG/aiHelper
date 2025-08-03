<template>
  <div class="chatbot-page">
    <div class="content">
      <h1>Merhaba <span class="wave">👋</span></h1>
      <p>Yardımcı olmamı ister misin? Sağ alttaki sohbet butonuna tıklayabilirsin.</p>
      <img
        src="https://cdn-icons-png.flaticon.com/512/4712/4712109.png"
        alt="Chatbot Illustration"
      />
    </div>

    <!-- Sohbet Butonu -->
    <button class="chat-button" @click="openChat = true">
      <img src="https://cdn-icons-png.flaticon.com/512/4712/4712109.png" alt="Chat" />
    </button>

    <!-- Büyük Chat Modalı -->
    <div v-if="openChat" class="chat-modal">
      <div class="chat-modal-content">
        <!-- Modal üst barı -->
        <div class="chat-header">
          <span class="chat-title">Sohbet</span>
          <button class="close-btn" @click="openChat = false">&times;</button>
        </div>
        <!-- Chat alanı (iframe ile) -->
        <iframe
          class="chatbot-iframe"
          src="https://yz.ulakbel.com/chatbot/133220bb-f71a-4953-ac20-9a50ff99e3cb"
          frameborder="0"
          allow="clipboard-write"
        ></iframe>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const openChat = ref(false)
</script>

<style scoped>
.chatbot-page {
  min-height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}

.content {
  text-align: center;
  max-width: 800px;
}

h1 {
  font-size: 4rem;
  color: #c9c9c9;
  margin-bottom: 1rem;
}

p {
  font-size: 1.5rem;
  color: #666;
  margin-bottom: 2rem;
}

img {
  width: 300px;
  max-width: 100%;
  opacity: 0.95;
}

.wave {
  display: inline-block;
  animation: wave 1.5s infinite;
}

@keyframes wave {
  0% { transform: rotate(0deg); }
  15% { transform: rotate(14deg); }
  30% { transform: rotate(-8deg); }
  45% { transform: rotate(14deg); }
  60% { transform: rotate(-4deg); }
  75% { transform: rotate(10deg); }
  100% { transform: rotate(0deg); }
}

/* Sohbet Butonu */
.chat-button {
  position: fixed;
  right: 32px;
  bottom: 32px;
  width: 64px;
  height: 64px;
  border-radius: 50%;
  background: #25d366;
  border: none;
  box-shadow: 0 4px 16px rgba(0,0,0,0.2);
  cursor: pointer;
  z-index: 1001;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.2s;
}
.chat-button img {
  width: 40px;
  height: 40px;
  display: block;
  margin-left: 6px; /* veya ihtiyaca göre 12px, 16px */
}
.chat-button:hover {
  background: #20ba5a;
}

/* Chat Modalı */
.chat-modal {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.35);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2000;
}
.chat-modal-content {
  width: 90vw;
  max-width: 900px;
  height: 80vh;
  background: #f0f2f5;
  border-radius: 16px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.18);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Modal üst barı */
.chat-header {
  height: 56px;
  background: #075e54;
  color: #fff;
  display: flex;
  align-items: center;
  padding: 0 24px;
  font-size: 1.3rem;
  font-weight: bold;
  justify-content: space-between;
}
.close-btn {
  background: transparent;
  border: none;
  color: #fff;
  font-size: 2rem;
  cursor: pointer;
}

/* Chat Alanı */
.chatbot-iframe {
  flex: 1;
  width: 100%;
  border: none;
  background: #fff;
}
@media (max-width: 600px) {
  .content {
    max-width: 98vw;
    padding: 0 8px;
  }

  h1 {
    font-size: 2rem;
    margin-bottom: 0.5rem;
  }

  p {
    font-size: 1rem;
    margin-bottom: 1rem;
  }

  img {
    width: 120px;
    margin-bottom: 1rem;
  }

  .chat-button {
    width: 48px;
    height: 48px;
    right: 12px;
    bottom: 12px;
  }
  .chat-button img {
    width: 28px;
    height: 28px;
    margin-right: 3px; 
    margin-top: 15px; 
  }

  .chat-modal-content {
    width: 100vw;
    max-width: 100vw;
    height: 100vh;
    border-radius: 0;
  }

  .chat-header {
    height: 44px;
    font-size: 1rem;
    padding: 0 10px;
  }

  .close-btn {
    font-size: 1.5rem;
  }
}
</style>