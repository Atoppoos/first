<template>
  <div class="scifi-container">
    <!-- 背景网格与扫描线 -->
    <div class="grid-bg"></div>
    <div class="scanline"></div>

    <!-- 全息投影主体 -->
    <div class="hologram">
      <!-- 顶部装饰条 -->
      <div class="top-bar">
        <span class="blink-dot"></span>
        <span class="status-text">SYSTEM ONLINE // NODE: 7A-9</span>
      </div>

      <!-- 主文字输出区 -->
      <div class="main-display">
        <p class="prompt">> INITIALIZING QUANTUM CORE...</p>
        <p class="prompt">> LOADING PROTOCOL: HELLO_WORLD.EXE</p>

        <!-- 核心的 Hello World 发光文字 -->
        <h1 class="glitch-text" data-text="HELLO, WORLD">HELLO, WORLD</h1>

        <p class="output">> PROCESS COMPLETE. AWAITING INPUT...</p>
      </div>

      <!-- 底部进度条与数据 -->
      <div class="bottom-bar">
        <div class="progress-bar">
          <div class="progress-fill" :style="{ width: progress + '%' }"></div>
        </div>
        <div class="data-stream">
          <span v-for="(val, index) in dataStream" :key="index">{{ val }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SciFiHelloWorld",
  data() {
    return {
      progress: 0,
      dataStream: ["0x7F", "0x3A", "0xFF", "0x01", "0x9C", "0x4E"],
      progressInterval: null,
      dataInterval: null,
    };
  },
  mounted() {
    // 进度条动画
    this.progressInterval = setInterval(() => {
      if (this.progress < 100) {
        this.progress += Math.floor(Math.random() * 5) + 1;
        if (this.progress > 100) this.progress = 100;
      }
    }, 200);

    // 模拟数据流跳动
    this.dataInterval = setInterval(() => {
      this.dataStream = this.dataStream.map(
        () =>
          "0x" +
          Math.floor(Math.random() * 255)
            .toString(16)
            .toUpperCase()
            .padStart(2, "0"),
      );
    }, 500);
  },
  beforeDestroy() {
    // 清理定时器，防止内存泄漏
    if (this.progressInterval) clearInterval(this.progressInterval);
    if (this.dataInterval) clearInterval(this.dataInterval);
  },
};
</script>

<style scoped>
/* 引入科幻感字体 */
@import url("https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap");

.scifi-container {
  position: relative;
  width: 100%;
  min-height: 100vh;
  background-color: #050a0f;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  font-family: "Share Tech Mono", monospace;
  color: #00ffff;
}

/* 背景网格 */
.grid-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image:
    linear-gradient(rgba(0, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 30px 30px;
  z-index: 1;
}

/* 扫描线特效 */
.scanline {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    to bottom,
    transparent 50%,
    rgba(0, 255, 255, 0.1) 51%
  );
  background-size: 100% 4px;
  z-index: 2;
  pointer-events: none;
  animation: scan 10s linear infinite;
}

@keyframes scan {
  0% {
    background-position: 0 0;
  }
  100% {
    background-position: 0 100vh;
  }
}

/* 全息投影面板 */
.hologram {
  position: relative;
  z-index: 10;
  width: 90%;
  max-width: 600px;
  padding: 20px;
  border: 1px solid rgba(0, 255, 255, 0.3);
  background: rgba(0, 20, 30, 0.7);
  box-shadow:
    0 0 20px rgba(0, 255, 255, 0.2),
    inset 0 0 30px rgba(0, 255, 255, 0.1);
  backdrop-filter: blur(5px);
  border-radius: 4px;
}

/* 顶部状态栏 */
.top-bar {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
  border-bottom: 1px solid rgba(0, 255, 255, 0.2);
  padding-bottom: 10px;
}

.blink-dot {
  width: 8px;
  height: 8px;
  background-color: #00ffff;
  border-radius: 50%;
  animation: blink 1s infinite alternate;
  box-shadow: 0 0 10px #00ffff;
}

@keyframes blink {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0.2;
  }
}

.status-text {
  font-size: 12px;
  color: #66ffff;
  letter-spacing: 2px;
}

/* 主显示区 */
.main-display {
  margin-bottom: 20px;
}

.prompt,
.output {
  font-size: 14px;
  color: #66ffff;
  margin: 5px 0;
  text-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
}

/* 核心 Glitch 文字特效 */
.glitch-text {
  position: relative;
  font-size: 3rem;
  font-weight: bold;
  margin: 20px 0;
  color: #ffffff;
  text-shadow:
    0 0 10px #00ffff,
    0 0 20px #00ffff,
    0 0 40px #00ffff;
  letter-spacing: 4px;
  animation: textFlicker 3s infinite alternate;
}

@keyframes textFlicker {
  0%,
  19%,
  21%,
  23%,
  25%,
  54%,
  56%,
  100% {
    opacity: 1;
    text-shadow:
      0 0 10px #00ffff,
      0 0 20px #00ffff,
      0 0 40px #00ffff;
  }
  20%,
  24%,
  55% {
    opacity: 0.5;
    text-shadow: none;
  }
}

/* 底部进度与数据 */
.bottom-bar {
  border-top: 1px solid rgba(0, 255, 255, 0.2);
  padding-top: 15px;
}

.progress-bar {
  width: 100%;
  height: 4px;
  background: rgba(0, 255, 255, 0.1);
  border-radius: 2px;
  overflow: hidden;
  margin-bottom: 10px;
}

.progress-fill {
  height: 100%;
  background: #00ffff;
  box-shadow: 0 0 10px #00ffff;
  transition: width 0.3s ease;
}

.data-stream {
  display: flex;
  justify-content: space-between;
  font-size: 10px;
  color: rgba(0, 255, 255, 0.6);
}
</style>
