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
  </div>
</template>

<script type="module">
    import Chatbot from "https://cdn.jsdelivr.net/npm/flowise-embed/dist/web.js"
    Chatbot.init({
        chatflowid: "133220bb-f71a-4953-ac20-9a50ff99e3cb",
        apiHost: "https://yz.ulakbel.com",
    })
</script>

<style scoped>
.chatbot-page {

  min-height: 100vh;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

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
</style>
