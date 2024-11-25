<script setup lang="ts"></script>

<template>
  <main class="container">
    <div class="content">
      <h1 class="title">PWA Example by 920OJ</h1>

      <div class="card">
        <p class="text">このアプリはPWAに対応しており、ホーム画面に追加することができます。</p>
        <p class="text">
          ホーム画面に追加するには、このページをブラウザの共有メニューから「ホーム画面に追加」を選択してください。
        </p>
      </div>

      <div class="card">
        <h2 class="subtitle">天気予報</h2>
        <div class="link-container">
          <router-link to="/weather/130010" class="link-button">
            <span class="icon">🏢</span>
            東京（会社）
          </router-link>
          <router-link to="/weather/140010" class="link-button">
            <span class="icon">🏚️</span>
            横浜（家）
          </router-link>
          <router-link to="/weather/230010" class="link-button">
            <span class="icon">🏠</span>
            愛知（実家）
          </router-link>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.container {
  min-height: 100vh;
  background: linear-gradient(to bottom right, #f0f4ff, #e6eeff);
  padding: 2rem;
}

.content {
  max-width: 800px;
  margin: 0 auto;
}

.title {
  font-size: 1.5rem;
  color: #1a237e;
  margin-bottom: 2rem;
  font-weight: bold;
}

.subtitle {
  font-size: 1.5rem;
  color: #1a237e;
  margin-bottom: 1rem;
  font-weight: 600;
}

.card {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.text {
  color: #333;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.text:last-child {
  margin-bottom: 0;
}

.link-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.link-button {
  display: flex;
  align-items: center;
  padding: 0.75rem 1rem;
  background-color: #3f51b5;
  color: white;
  text-decoration: none;
  border-radius: 8px;
  transition: background-color 0.2s;
}

.link-button:hover {
  background-color: #283593;
}

.icon {
  margin-right: 0.5rem;
  font-size: 1.2rem;
}
</style>
