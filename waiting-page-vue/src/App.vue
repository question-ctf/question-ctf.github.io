<template>
  <div id="app">
    <header>
      <img src="/favicon.ico" alt="Favicon" class="favicon">
      <h1>?CTF 2025</h1>
    </header>
    <main>
      <div class="countdown-container">
        <div class="countdown-item orange">
          <h2>校内赛道</h2>
          <div class="start-time">开始时间：2025年9月27日 10:00 (UTC+8)</div>
          <div class="timer">
            <div class="time-box">
              <span class="time">{{ internal.days }}</span>
              <span class="label">天</span>
            </div>
            <div class="time-box">
              <span class="time">{{ internal.hours }}</span>
              <span class="label">时</span>
            </div>
            <div class="time-box">
              <span class="time">{{ internal.minutes }}</span>
              <span class="label">分</span>
            </div>
            <div class="time-box">
              <span class="time">{{ internal.seconds }}</span>
              <span class="label">秒</span>
            </div>
          </div>
        </div>
        <div class="countdown-item blue">
          <h2>校外赛道</h2>
          <div class="start-time">开始时间：2025年10月4日 10:00 (UTC+8)</div>
          <div class="timer">
            <div class="time-box">
              <span class="time">{{ external.days }}</span>
              <span class="label">天</span>
            </div>
            <div class="time-box">
              <span class="time">{{ external.hours }}</span>
              <span class="label">时</span>
            </div>
            <div class="time-box">
              <span class="time">{{ external.minutes }}</span>
              <span class="label">分</span>
            </div>
            <div class="time-box">
              <span class="time">{{ external.seconds }}</span>
              <span class="label">秒</span>
            </div>
          </div>
        </div>
      </div>
      <div class="info-container">
        <div class="info-section">
          <h3>平台通知</h3>
          <p>这是 ?CTF 2025 的预热页面。正式比赛平台正在维护中。</p>
        </div>
        <div class="info-section">
          <h3>联系我们</h3>
          <p>公开赛道群：1063409268</p>
          <p>校内赛道：由各高校独立通知</p>
        </div>
      </div>
      <div class="about-section">
        <h2>关于 ?CTF 2025</h2>
        <p>?CTF 2025 是由来自杭州师范大学、暨南大学、广东工业大学、哈尔滨理工大学、湖南科技大学、西安工业大学、福建农林大学、太原理工大学、浙江师范大学、江南大学、山东科技大学、东北大学秦皇岛分校、青岛工学院、广东外语外贸大学、兰州大学（以上排名不分先后）共十五所高校的网络安全竞赛团队共同发起的CTF新生赛。</p>
        <p>比赛采取传统 Jeopardy 解题个人赛的形式，持续四周时间，每周放出新赛题，同时停止上一周赛题作答。大部分赛题采用动态计分，其涵盖 Web、Reverse、Pwn、Crypto、Misc 五大方向。</p>
        <p>本赛事设置校内赛道供联办高校招新选拔参考使用，同时设置公开赛道，希望与全国各地的师傅交流学习，共同进步。</p>
        <p>🙏 ?CTF 作为一个完全公益的新赛事，其筹备历程颇为艰难，各种不周之处，万望海涵。🙏</p>
      </div>
    </main>
    <footer>
      <p>Copyright © 2025 ?CTF 赛事组委会</p>
      <p>浙ICP备2025198404号</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      internal: {
        days: '00',
        hours: '00',
        minutes: '00',
        seconds: '00',
      },
      external: {
        days: '00',
        hours: '00',
        minutes: '00',
        seconds: '00',
      },
      internalTarget: new Date('2025-09-27T10:00:00+08:00').getTime(),
      externalTarget: new Date('2025-10-04T10:00:00+08:00').getTime(),
      timerInterval: null,
    };
  },
  methods: {
    updateCountdown() {
      const now = new Date().getTime();

      // Internal
      const internalDistance = this.internalTarget - now;
      this.internal.days = Math.floor(internalDistance / (1000 * 60 * 60 * 24)).toString().padStart(2, '0');
      this.internal.hours = Math.floor((internalDistance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)).toString().padStart(2, '0');
      this.internal.minutes = Math.floor((internalDistance % (1000 * 60 * 60)) / (1000 * 60)).toString().padStart(2, '0');
      this.internal.seconds = Math.floor((internalDistance % (1000 * 60)) / 1000).toString().padStart(2, '0');

      // External
      const externalDistance = this.externalTarget - now;
      this.external.days = Math.floor(externalDistance / (1000 * 60 * 60 * 24)).toString().padStart(2, '0');
      this.external.hours = Math.floor((externalDistance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60)).toString().padStart(2, '0');
      this.external.minutes = Math.floor((externalDistance % (1000 * 60 * 60)) / (1000 * 60)).toString().padStart(2, '0');
      this.external.seconds = Math.floor((externalDistance % (1000 * 60)) / 1000).toString().padStart(2, '0');

      if (internalDistance < 0) {
        this.internal = { days: '00', hours: '00', minutes: '00', seconds: '00' };
      }
      if (externalDistance < 0) {
        this.external = { days: '00', hours: '00', minutes: '00', seconds: '00' };
      }
    },
  },
  mounted() {
    this.updateCountdown();
    this.timerInterval = setInterval(this.updateCountdown, 1000);
  },
  beforeDestroy() {
    clearInterval(this.timerInterval);
  },
};
</script>

<style>
body {
  background: linear-gradient(135deg, #f0f8ff 0%, #e6f3ff 25%, #fff5ee 50%, #f0fff0 75%, #faf0e6 100%);
  color: #2c3e50;
  font-family: 'Orbitron', 'Roboto Mono', monospace;
  text-align: center;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  position: relative;
  animation: backgroundShift 10s ease-in-out infinite;
  min-height: 100vh;
}

@keyframes backgroundShift {
  0%, 100% {
    background: linear-gradient(135deg, #f0f8ff 0%, #e6f3ff 25%, #fff5ee 50%, #f0fff0 75%, #faf0e6 100%);
  }
  50% {
    background: linear-gradient(135deg, #fff5ee 0%, #f0fff0 25%, #f0f8ff 50%, #faf0e6 75%, #e6f3ff 100%);
  }
}

body::before {
  content: '';
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-image: 
    radial-gradient(circle at 20% 20%, rgba(255, 107, 53, 0.1) 0%, transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(52, 152, 219, 0.1) 0%, transparent 40%),
    radial-gradient(circle at 60% 40%, rgba(155, 89, 182, 0.08) 0%, transparent 35%),
    conic-gradient(from 0deg at 50% 50%, transparent 0deg, rgba(46, 204, 113, 0.05) 90deg, transparent 180deg, rgba(231, 76, 60, 0.05) 270deg, transparent 360deg);
  pointer-events: none;
  z-index: -1;
  animation: patternRotate 20s linear infinite;
}

@keyframes patternRotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

#app {
  font-family: 'Orbitron', 'Roboto Mono', monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-start;
  min-height: calc(100vh - 2rem);
  margin: 1rem auto;
  padding: 2rem 1rem 1rem 1rem;
  border: 3px solid transparent;
  border-radius: 25px;
  background: 
    linear-gradient(white, white) padding-box,
    linear-gradient(45deg, #ff6b35, #3498db, #9b59b6, #2ecc71, #e74c3c) border-box;
  box-shadow: 
    0 10px 30px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(255, 255, 255, 0.8),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  position: relative;
  animation: containerFloat 6s ease-in-out infinite;
  box-sizing: border-box;
  max-width: 1200px;
}

@media (max-width: 768px) {
  #app {
    padding: 1rem 0.5rem 0.5rem 0.5rem;
    margin: 0.5rem auto;
    min-height: calc(100vh - 1rem);
  }
  
  header {
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
  }
  
  header h1 {
    font-size: 2rem;
    margin: 0;
  }
  
  .favicon {
    width: 40px;
    height: 40px;
    margin-right: 0;
    margin-bottom: 0.5rem;
  }
  
  .countdown-container {
    flex-direction: column;
    gap: 1rem;
    margin: 1rem 0;
  }
  
  .countdown-item {
    padding: 1rem;
  }
  
  .countdown-item h2 {
    font-size: 1.3rem;
    padding: 0.5rem;
    margin-bottom: 0.5rem;
  }
  
  .start-time {
    font-size: 0.8rem;
    padding: 0.4rem 0.8rem;
    margin-bottom: 0.8rem;
  }
  
  .timer {
    gap: 0.5rem;
  }
  
  .time-box {
    padding: 0.5rem;
  }
  
  .time {
    font-size: 1.5rem !important;
  }
  
  .label {
    font-size: 0.8rem;
  }
  
  .info-container {
    flex-direction: column;
    gap: 1rem;
    margin: 1rem 0;
  }
  
  .info-section {
    padding: 1.5rem;
  }
  
  .info-section h3 {
    font-size: 1.2rem;
  }
  
  .about-section {
    padding: 1.5rem;
    margin-top: 1rem;
  }
  
  .about-section h2 {
    font-size: 1.4rem;
  }
  
  .about-section p {
    font-size: 0.9rem;
    line-height: 1.5;
  }
  
  footer {
    padding: 1rem;
    font-size: 0.8rem;
  }
}

@media (max-width: 480px) {
  #app {
    padding: 0.75rem 0.25rem 0.25rem 0.25rem;
    margin: 0.25rem;
    border-radius: 15px;
  }
  
  header h1 {
    font-size: 1.5rem;
    margin: 0;
  }
  
  .favicon {
    width: 30px;
    height: 30px;
  }
  
  .countdown-item h2 {
    font-size: 1.1rem;
  }
  
  .start-time {
    font-size: 0.75rem;
    padding: 0.3rem 0.6rem;
    margin-bottom: 0.6rem;
  }
  
  .time {
    font-size: 1.2rem !important;
  }
  
  .time-box {
    padding: 0.3rem;
  }
  
  .info-section {
    padding: 1rem;
  }
  
  .about-section {
    padding: 1rem;
  }
  
  .about-section h2 {
    font-size: 1.2rem;
  }
  
  .about-section p {
    font-size: 0.85rem;
  }
}

@keyframes containerFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  33% {
    transform: translateY(-10px) rotate(0.5deg);
  }
  66% {
    transform: translateY(5px) rotate(-0.5deg);
  }
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 1rem;
  margin-bottom: 1rem;
}

.favicon {
  width: 50px;
  height: 50px;
  margin-right: 1rem;
  filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.1));
  animation: faviconFloat 3s ease-in-out infinite;
}

@keyframes faviconFloat {
  0%, 100% {
    transform: translateY(0px) rotate(0deg);
  }
  33% {
    transform: translateY(-5px) rotate(2deg);
  }
  66% {
    transform: translateY(2px) rotate(-1deg);
  }
}

header h1 {
  font-size: 4rem;
  margin: 0;
  color: #2c3e50;
  font-weight: 700;
  letter-spacing: 3px;
  filter: drop-shadow(2px 2px 4px rgba(0, 0, 0, 0.1));
}



.countdown-container {
  display: flex;
  gap: 2rem;
}

.countdown-item {
  padding: 2rem;
  border: 2px solid;
  image-rendering: pixelated;
}

.countdown-item.orange {
  border-color: #ef761d;
}

.countdown-item.blue {
  border-color: #193285;
}

.countdown-item h2 {
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #e74c3c;
  background: linear-gradient(135deg, rgba(231, 76, 60, 0.1), rgba(255, 107, 53, 0.1));
  padding: 1.5rem 2rem;
  border-radius: 20px;
  border: 2px solid transparent;
  background-clip: padding-box;
  box-shadow: 
    0 8px 25px rgba(231, 76, 60, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
  font-weight: 600;
  animation: countdownPulse 2s ease-in-out infinite;
}

.start-time {
  font-size: 0.9rem;
  color: #7f8c8d;
  margin-bottom: 1rem;
  padding: 0.5rem 1rem;
  background: rgba(255, 255, 255, 0.6);
  border-radius: 10px;
  border: 1px solid rgba(52, 152, 219, 0.2);
  font-weight: 500;
}

@keyframes countdownPulse {
  0%, 100% {
    transform: scale(1);
    box-shadow: 0 8px 25px rgba(231, 76, 60, 0.2), inset 0 1px 0 rgba(255, 255, 255, 0.8);
  }
  50% {
    transform: scale(1.02);
    box-shadow: 0 12px 35px rgba(231, 76, 60, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.9);
  }
}

.timer {
  display: flex;
  gap: 1rem;
}

.time-box {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.time {
  font-size: 3rem;
  font-weight: bold;
}

.info-container {
  display: flex;
  justify-content: space-around;
  margin: 2rem 0;
  max-width: 800px;
  gap: 2rem;
}

.info-section {
  flex: 1;
  padding: 2rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.9), rgba(248, 249, 250, 0.8));
  border: 2px solid transparent;
  border-radius: 20px;
  background-clip: padding-box;
  box-shadow: 
    0 10px 30px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(52, 152, 219, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  position: relative;
  overflow: hidden;
}

.info-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(52, 152, 219, 0.1), transparent);
  transition: left 0.6s;
}

.info-section:hover {
  transform: translateY(-8px) scale(1.02);
  box-shadow: 
    0 20px 40px rgba(0, 0, 0, 0.15),
    0 0 0 1px rgba(52, 152, 219, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 1);
}

.info-section:hover::before {
  left: 100%;
}

.info-section h3 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
  background: linear-gradient(45deg, #e74c3c, #f39c12);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 600;
}

.info-section p {
  margin: 0;
  color: #34495e;
  line-height: 1.6;
}

footer p {
  margin: 0.2rem 0;
  font-size: 0.8rem;
  color: #888;
}

footer {
  margin-top: 2rem;
  font-size: 0.9rem;
  color: #7f8c8d;
  padding: 1.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.8), rgba(248, 249, 250, 0.6));
  border-radius: 15px;
  border: 1px solid rgba(52, 152, 219, 0.1);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
  backdrop-filter: blur(5px);
}

.about-section {
  margin-top: 2rem;
  padding: 2.5rem;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.95), rgba(248, 249, 250, 0.9));
  border: 3px solid transparent;
  border-radius: 25px;
  background-clip: padding-box;
  box-shadow: 
    0 15px 35px rgba(0, 0, 0, 0.1),
    0 0 0 1px rgba(155, 89, 182, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(15px);
  max-width: 800px;
  text-align: left;
  position: relative;
  overflow: hidden;
}

.about-section::before {
  content: '';
  position: absolute;
  top: -50%;
  left: -50%;
  width: 200%;
  height: 200%;
  background: conic-gradient(from 0deg, transparent, rgba(155, 89, 182, 0.05), transparent, rgba(46, 204, 113, 0.05), transparent);
  animation: sectionRotate 15s linear infinite;
  z-index: -1;
}

@keyframes sectionRotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.about-section h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
  text-align: center;
  background: linear-gradient(45deg, #9b59b6, #3498db);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  font-weight: 700;
}

.label {
  font-size: 1rem;
  color: #34495e;
  font-weight: 500;
}
</style>
