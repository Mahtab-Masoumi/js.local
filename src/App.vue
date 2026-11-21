
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const step = ref(1)

const persianNumber = (value) =>
  new Intl.NumberFormat('fa-IR').format(value)

const status = computed(() => {
  if (count.value > 0) return 'شمارنده در حال افزایش است'
  if (count.value < 0) return 'شمارنده در حالت منفی است'
  return 'شمارنده در نقطه شروع است'
})

const increase = () => {
  count.value += step.value
}

const decrease = () => {
  count.value -= step.value
}

const reset = () => {
  count.value = 0
}

const changeStep = (value) => {
  step.value = value
}
</script>

<template>
  <main class="page" dir="rtl">
    <div class="glow glow-one"></div>
    <div class="glow glow-two"></div>

    <section class="counter-card">

      <div class="header">
        <div class="icon-box">✦</div>
        <h1>شمارنده من</h1>
        <p>مدیریت اعداد با یک تجربه متفاوت!</p>
      </div>

      <div class="counter-box">
        <span class="number-label">مقدار فعلی</span>

        <div class="number">
          {{ persianNumber(count) }}
        </div>

        <div class="status">
          <span class="status-dot"></span>
          {{ status }}
        </div>
      </div>

      <div class="step-section">
        <span>میزان تغییر عدد</span>

        <div class="step-buttons">
          <button
            v-for="value in [1, 2, 5, 10]"
            :key="value"
            type="button"
            @click="changeStep(value)"
            :class="{ active: step === value }"
            :aria-pressed="step === value"
          >
            {{ persianNumber(value) }}
          </button>
        </div>
      </div>

      <div class="actions">
        <button
          type="button"
          class="action-btn increase"
          @click="increase"
        >
          <span>＋</span>
          افزایش
        </button>

        <button
          type="button"
          class="action-btn decrease"
          @click="decrease"
        >
          <span>－</span>
          کاهش
        </button>
      </div>

      <button
        type="button"
        class="reset-btn"
        @click="reset"
      >
        ↻ بازنشانی شمارنده
      </button>

    </section>
  </main>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Vazirmatn:wght@400;500;600;700;800&display=swap');

* {
  box-sizing: border-box;
}

.page {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
  position: relative;
  overflow: hidden;
  background: #080c1c;
  font-family: 'Vazirmatn', sans-serif;
}

.glow {
  position: absolute;
  width: 350px;
  height: 350px;
  border-radius: 50%;
  filter: blur(110px);
  opacity: 0.35;
  pointer-events: none;
}

.glow-one {
  background: #853bff;
  top: -100px;
  right: -80px;
}

.glow-two {
  background: #00d5c0;
  bottom: -100px;
  left: -80px;
}

.counter-card {
  position: relative;
  z-index: 1;
  width: 100%;
  max-width: 430px;
  padding: 32px;
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 28px;
  background: rgba(20, 27, 52, 0.88);
  box-shadow: 0 25px 80px rgba(0,0,0,0.4);
  backdrop-filter: blur(20px);
  color: white;
  transition: transform 0.35s, box-shadow 0.35s;
}

.counter-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 30px 90px rgba(113, 70, 255, 0.17);
}

.header {
  text-align: center;
}

.icon-box {
  width: 55px;
  height: 55px;
  margin: auto;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 18px;
  background: linear-gradient(135deg, #854bff, #4e9dff);
  font-size: 28px;
  box-shadow: 0 8px 25px rgba(112, 75, 255, 0.4);
}

.header h1 {
  font-size: 27px;
  margin: 15px 0 5px;
  font-weight: 800;
}

.header p {
  font-size: 13px;
  color: #9ba7c3;
  margin: 0 0 25px;
}

.counter-box {
  background: linear-gradient(
    145deg,
    rgba(119, 77, 255, 0.16),
    rgba(0, 213, 192, 0.08)
  );
  border: 1px solid rgba(255,255,255,0.1);
  border-radius: 22px;
  padding: 22px;
  text-align: center;
}

.number-label {
  color: #aebbd6;
  font-size: 13px;
}

.number {
  font-size: clamp(45px, 12vw, 65px);
  font-weight: 800;
  color: #fff;
  margin: 5px 0;
  text-shadow: 0 0 25px rgba(133, 75, 255, 0.45);
  overflow-wrap: anywhere;
  transition: 0.2s;
}

.status {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  color: #a5f3e9;
}

.status-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #00e6c3;
  box-shadow: 0 0 12px #00e6c3;
}

.step-section {
  margin: 25px 0 18px;
}

.step-section > span {
  display: block;
  font-size: 13px;
  color: #b8c3dc;
  margin-bottom: 12px;
}

.step-buttons {
  display: flex;
  gap: 10px;
}

.step-buttons button {
  flex: 1;
  padding: 10px;
  border: 1px solid #343e5d;
  border-radius: 12px;
  background: #1c2542;
  color: #bdc8e0;
  font-family: inherit;
  cursor: pointer;
  transition: 0.25s;
}

.step-buttons button:hover {
  border-color: #9a6aff;
  color: white;
  transform: translateY(-3px);
}

.step-buttons button.active {
  background: linear-gradient(135deg, #814bff, #a05cff);
  color: white;
  border-color: transparent;
  box-shadow: 0 5px 18px rgba(129,75,255,0.3);
}

.actions {
  display: flex;
  gap: 12px;
  margin-top: 20px;
}

.action-btn {
  flex: 1;
  border: none;
  border-radius: 14px;
  padding: 14px 10px;
  color: white;
  font-family: inherit;
  font-weight: 700;
  font-size: 14px;
  cursor: pointer;
  transition: 0.3s;
}

.action-btn span {
  font-size: 19px;
  margin-left: 5px;
}

.increase {
  background: linear-gradient(135deg, #00bfa6, #00d9bd);
  box-shadow: 0 7px 20px rgba(0,217,189,0.17);
}

.decrease {
  background: linear-gradient(135deg, #7450e8, #9b5bff);
  box-shadow: 0 7px 20px rgba(155,91,255,0.2);
}

.action-btn:hover {
  transform: translateY(-4px);
  filter: brightness(1.15);
}

.action-btn:active {
  transform: scale(0.96);
}

.reset-btn {
  width: 100%;
  margin-top: 13px;
  padding: 12px;
  border: 1px solid rgba(255,255,255,0.12);
  border-radius: 13px;
  background: rgba(255,255,255,0.04);
  color: #aebbd6;
  font-family: inherit;
  cursor: pointer;
  transition: 0.3s;
}

.reset-btn:hover {
  background: rgba(255, 95, 122, 0.13);
  color: #ff8299;
  border-color: rgba(255,95,122,0.35);
}

@media (max-width: 480px) {
  .counter-card {
    padding: 24px 18px;
  }

  .header h1 {
    font-size: 23px;
  }
}
</style>
