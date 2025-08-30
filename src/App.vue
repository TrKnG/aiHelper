<template>
  <div :class="['chatbot-page', darkMode ? 'dark' : 'light', openChat ? 'open-chat' : '']">
    <!-- Tema butonu sadece sohbet kapalıyken DOM'da -->
    <div class="theme-toggle" v-if="!openChat">
      <button @click="toggleDarkMode" :aria-label="darkMode ? 'Açık tema' : 'Koyu tema'">
        <span v-if="darkMode">🌞</span>
        <span v-else>🌙</span>
      </button>
    </div>
    <div class="content">
      <div class="content-inner">
        <div class="text-block">
          <h1>Merhaba <span class="wave">👋</span></h1>
          <p class="intro-text">
            Yardımcı olmamı ister misin? Sağ alttaki sohbet butonuna tıklayabilirsin.
          </p>
        </div>
        <img
          class="bot-img"
          src="https://cdn-icons-png.flaticon.com/512/4712/4712109.png"
          alt="Chatbot Illustration"
        />
      </div>
    </div>

    <!-- Sohbet Butonu -->
    <button class="chat-button" @click="openChat = true" aria-label="Sohbeti Aç">
      <img src="https://cdn-icons-png.flaticon.com/512/4712/4712109.png" alt="Chat" />
    </button>

    <!-- Büyük Chat Modalı -->
    <transition name="modal-fade">
      <div v-if="openChat" class="chat-modal" @click.self="closeChat">
        <div class="chat-modal-content">
          <div class="chat-header">
            <span class="chat-title">Sohbet</span>
            <button class="close-btn" @click="closeChat" aria-label="Kapat">&times;</button>
          </div>
          <div class="chatbot-iframe-wrapper">
            <transition name="spinner-fade">
              <div v-if="!isIframeLoaded" class="spinner-wrapper">
                <div class="spinner"></div>
              </div>
            </transition>
            <iframe
              v-show="isIframeLoaded"
              class="chatbot-iframe"
              src="https://yz.ulakbel.com/chatbot/133220bb-f71a-4953-ac20-9a50ff99e3cb"
              frameborder="0"
              allow="microphone; camera; autoplay; clipboard-write"
              @load="onIframeLoad"
              title="Chatbot"
            ></iframe>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
const openChat = ref(false)
const isIframeLoaded = ref(false)
const darkMode = ref(true)

function onIframeLoad() {
  isIframeLoaded.value = true
}
function closeChat() {
  openChat.value = false
  isIframeLoaded.value = false
}
function toggleDarkMode() {
  darkMode.value = !darkMode.value
}

// EKSTRA GARANTİ: body'ye class ekle
watch(openChat, (val) => {
  if (val) {
    document.body.classList.add('open-chat');
  } else {
    document.body.classList.remove('open-chat');
  }
});
</script>

<style scoped>
/* Temalar */
.chatbot-page.light {
  background: linear-gradient(135deg, #e0f7fa 0%, #d1eaff 50%, #f0f2f5 100%);
  color: #222;
}
.chatbot-page.dark {
  background: linear-gradient(135deg, #23272f 0%, #22242c 100%);
  color: #eee;
}

/* Tema butonu */
.theme-toggle {
  position: fixed;
  top: 18px;
  right: 24px;
  z-index: 10 !important; /* Modalın altında kalır */
}
.theme-toggle button {
  background: none;
  border: none;
  font-size: 2rem;
  cursor: pointer;
  color: inherit;
  transition: filter 0.1s;
  filter: drop-shadow(0 0 3px #0008);
}
.theme-toggle button:active {
  filter: brightness(1.3);
}
/* EKSTRA GARANTİ: Sohbet açıkken tema butonunu her yerde gizle */
body.open-chat .theme-toggle { display: none !important; }
.open-chat .theme-toggle { display: none !important; }

/* İçerik */
.content {
  width: 100vw;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 0;
}
.content-inner {
  display: flex;
  flex-direction: row;
  align-items: center;
  background: rgba(30,30,40,0.93);
  border-radius: 32px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.18);
  padding: 3.5rem 3rem 2.5rem 2.5rem;
  margin: 2.5rem 0;
  min-width: 340px;
  max-width: 600px;
  animation: card-pop 0.7s cubic-bezier(.3,1.5,.5,1) 1;
}
.chatbot-page.light .content-inner {
  background: rgba(255,255,255,0.97);
}
.text-block {
  flex: 1;
  text-align: left;
}
h1 {
  font-size: 3.2rem;
  color: #ffe082;
  margin-bottom: 1.1rem;
  font-weight: 800;
  letter-spacing: -1px;
  line-height: 1.1;
}
.chatbot-page.light h1 {
  color: #1a3a40;
}
.intro-text, p {
  font-size: 1.15rem;
  color: #b0bec5;
  margin-bottom: 1.5rem;
  font-weight: 500;
  line-height: 1.3;
  max-width: 32ch;
}
.chatbot-page.light .intro-text, .chatbot-page.light p {
  color: #24716c;
}
.bot-img {
  width: 140px;
  max-width: 34vw;
  min-width: 90px;
  opacity: 0.98;
  margin-left: 2.2rem;
  filter: drop-shadow(0 2px 8px #25d36644);
  align-self: flex-end;
}
.wave {
  display: inline-block;
  animation: wave 1.5s infinite;
  filter: drop-shadow(0 0 4px #fff176);
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
@keyframes card-pop {
  0% { transform: scale(0.95) translateY(30px); opacity: 0; }
  100% { transform: scale(1) translateY(0); opacity: 1; }
}

/* Sohbet Butonu */
.chat-button {
  position: fixed;
  right: 32px;
  bottom: 32px;
  width: 68px;
  height: 68px;
  border-radius: 50%;
  background: linear-gradient(135deg,#25d366 60%,#128c7e 100%);
  border: none;
  box-shadow: 0 4px 16px rgba(0,0,0,0.23);
  cursor: pointer;
  z-index: 1001;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.18s, transform 0.13s;
  animation: pulse 2.2s infinite;
}
@keyframes pulse {
  0% { box-shadow: 0 0 0 0 #25d36644; }
  70% { box-shadow: 0 0 0 14px #25d36600; }
  100% { box-shadow: 0 0 0 0 #25d36600; }
}
.chat-button img {
  width: 40px;
  height: 40px;
  display: block;
  margin-left: 4px;
}
.chat-button:active {
  transform: scale(0.93);
}
.chat-button:hover {
  background: linear-gradient(135deg,#20ba5a 60%,#128c7e 100%);
}

/* Modal fade animasyonu */
.modal-fade-enter-active, .modal-fade-leave-active {
  transition: opacity 0.22s;
}
.modal-fade-enter-from, .modal-fade-leave-to {
  opacity: 0;
}

/* Chat Modalı */
.chat-modal {
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0,0,0,0.33);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999 !important; /* Yüksek bir değer! */
}
@keyframes modal-pop {
  0% { opacity: 0; transform: scale(0.97);}
  100% { opacity: 1; transform: scale(1);}
}
.chat-modal-content {
  width: 99vw;
  max-width: 1100px;
  height: 96vh;
  background: #23272f;
  border-radius: 22px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.17);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  animation: modal-content-pop 0.4s cubic-bezier(.3,1.5,.5,1);
}
.chatbot-page.light .chat-modal-content {
  background: #f0f2f5;
}
@keyframes modal-content-pop {
  0% { transform: translateY(30px); opacity: 0;}
  100% { transform: translateY(0); opacity: 1;}
}
.chat-header {
  height: 62px;
  background: linear-gradient(90deg,#075e54 70%,#128c7e 100%);
  color: #fff;
  display: flex;
  align-items: center;
  padding: 0 30px;
  font-size: 1.45rem;
  font-weight: bold;
  justify-content: space-between;
  letter-spacing: 0.5px;
  box-shadow: 0 2px 8px #075e5422;
}
.close-btn {
  background: transparent;
  border: none;
  color: #fff;
  font-size: 2.2rem;
  cursor: pointer;
  transition: color 0.14s;
}
.close-btn:hover {
  color: #ffb300;
}
.chatbot-iframe-wrapper {
  position: relative;
  width: 100%;
  flex: 1;
  display: flex;
  background: #fff;
}
.chatbot-page.dark .chatbot-iframe-wrapper {
  background: #23272f;
}
.spinner-fade-enter-active, .spinner-fade-leave-active {
  transition: opacity 0.22s;
}
.spinner-fade-enter-from, .spinner-fade-leave-to {
  opacity: 0;
}
.spinner-wrapper {
  position: absolute;
  top: 0; left: 0; right: 0; bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #fff;
  z-index: 1;
}
.chatbot-page.dark .spinner-wrapper {
  background: #23272f;
}
.spinner {
  width: 54px;
  height: 54px;
  border: 7px solid #eee;
  border-top: 7px solid #25d366;
  border-radius: 50%;
  animation: spin 0.8s cubic-bezier(0.4, 0, 0.2, 1) infinite;
}
.chatbot-iframe {
  flex: 1;
  width: 100%;
  border: none;
  background: transparent;
  min-height: 0;
}

/* Mobil uyum */
@media (max-width: 900px) {
  .content-inner {
    flex-direction: column;
    align-items: center;
    padding: 2.2rem 1.2rem 1.5rem 1.2rem;
    max-width: 98vw;
  }
  .bot-img {
    margin: 1.2rem 0 0 0;
    align-self: center;
    width: 110px;
    min-width: 60px;
  }
  .text-block {
    text-align: center;
    width: 100%;
  }
}
@media (max-width: 600px) {
  .content-inner {
    flex-direction: column;
    align-items: center;
    padding: 2.2rem 0.7rem 2.2rem 0.7rem;
    margin: 0.7rem 0;
    width: 100vw !important;
    max-width: 100vw !important;
    height: 100vh !important;
    border-radius: 0 !important;
  }
  h1 {
    font-size: 2rem;
    margin-bottom: 0.7rem;
    text-align: center;
  }
  .intro-text, p {
    font-size: 1.1rem;
    margin-bottom: 1.2rem;
    max-width: 90vw;
    text-align: center;
  }
  .bot-img {
    width: 90px;
    margin: 1.3rem 0 0 0;
    align-self: center;
  }
  .chat-button {
    width: 54px;
    height: 54px;
    right: 12px;
    bottom: 12px;
  }
  .chat-button img {
    width: 32px;
    height: 32px;
    margin-left: 2px;
  }
  .chat-modal-content {
    width: 100vw;
    max-width: 100vw;
    height: 100vh;
    border-radius: 0;
  }
  .chat-header {
    height: 44px;
    font-size: 1.1rem;
    padding: 0 10px;
  }
  .close-btn {
    font-size: 1.5rem;
  }
}
</style>
