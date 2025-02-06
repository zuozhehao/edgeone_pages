<template>
    <div class="container">
        <div class="content">
            <h1 class="title animate__animated animate__fadeIn">{{ target_domain }}</h1>
            <p class="subtitle">Design • Develop • Innovate</p>
            <div v-for="(dot, index) in dots" :key="index" class="floating-dot" :style="dot.style"></div>
        </div>
        <a v-if="target_beian" href="https://beian.miit.gov.cn" target="_blank" class="record-number">{{ target_beian }}</a>
    </div>
</template>

<script>
export default {
    data() {
        return {
            dots: Array(20).fill(null).map(() => ({
                style: {
                    left: Math.random() * 100 + '%',
                    top:  Math.random() * 100 + '%',
                    animationDelay: Math.random() * 1 + 's'
                }
            })),
            target_beian: '',
            target_domain: ''
        };
    },
    mounted() {
      const hostname     = window.location.hostname;
      const domain       = hostname.split('.').slice(-2).join('.');
      const value        = domain.replace('.', '_').toUpperCase();
      this.target_domain = domain;
      this.target_beian  = import.meta.env[`VITE_BEIAN_${value}`] || '';
      console.log(import.meta.env);
    }
};
</script>


<style scoped>
.container {
  min-height: 100vh;
  background: linear-gradient(45deg, #0f0c29, #302b63, #24243e);
  position: relative;
  overflow: hidden;
}

.content {
  padding: 2rem;
  text-align: center;
  z-index: 1;
  min-height: calc(100vh - 100px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.title {
  font-size: 4rem;
  color: rgba(255,255,255,0.9);
  text-shadow: 0 0 20px rgba(255,255,255,0.3);
  margin-bottom: 1rem;
  font-family: 'Arial Rounded MT Bold', sans-serif;
}

.subtitle {
  color: #7f7fd5;
  font-size: 1.5rem;
  letter-spacing: 4px;
  position: relative;
}

.floating-dot {
  position: absolute;
  width: 8px;
  height: 8px;
  background: rgba(255,255,255,0.15);
  border-radius: 50%;
  animation: float 8s infinite linear;
  pointer-events: none;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0) scale(1);
    opacity: 0.3;
  }
  50% {
    transform: translateY(-40px) scale(0.8);
    opacity: 0.1;
  }
}

.record-number {
  position: absolute;
  bottom: 15vh;
  left: 50%;
  transform: translateX(-50%);
  color: rgba(255,255,255,0.6);
  text-decoration: none;
  font-size: 0.9rem;
  padding: 8px 15px;
  border-radius: 20px;
  background: rgba(0,0,0,0.3);
  transition: all 0.3s ease;
}

.record-number:hover {
  background: rgba(255,255,255,0.1);
  color: #7f7fd5;
  transform: translateX(-50%) translateY(-2px);
  box-shadow: 0 2px 10px rgba(127,127,213,0.2);
}

@media (max-width: 768px) {
  .title {
    font-size: 2.5rem;
  }
  
  .subtitle {
    font-size: 1.2rem;
  }
  
  .record-number {
    font-size: 0.8rem;
    bottom: 10vh;
  }
}
</style>
