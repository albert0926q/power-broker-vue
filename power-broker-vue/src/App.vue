<script setup>
import { ref, onMounted } from 'vue'

const activeSection = ref('home')

const services = [
  { icon: '🔍', title: '信息匹配', desc: '深入了解供需双方需求，精准匹配最合适的算力资源' },
  { icon: '🌐', title: '需求翻译', desc: '专业团队帮您翻译技术需求，消除语言障碍' },
  { icon: '🤝', title: '协调沟通', desc: '全程跟进协调，解决合作过程中的各类问题' },
  { icon: '📋', title: '方案定制', desc: '根据您的具体需求，量身定制最优解决方案' }
]

const advantages = [
  { icon: '🌍', title: '中英文双语', desc: '专业双语团队，无缝沟通国内外客户' },
  { icon: '⚡', title: '24小时响应', desc: '全天候服务，及时响应您的每一步需求' },
  { icon: '💻', title: '懂技术更专业', desc: '深厚技术背景，准确理解各类技术需求' },
  { icon: '💰', title: '价格透明', desc: '明码标价，让您每一分钱都花得明白' }
]

const process = [
  { step: '1', title: '提交需求', desc: '填写联系方式和需求' },
  { step: '2', title: '需求分析', desc: '专业团队评估需求' },
  { step: '3', title: '方案制定', desc: '提供定制化解决方案' },
  { step: '4', title: '双方对接', desc: '协助供需双方沟通' },
  { step: '5', title: '合同签订', desc: '明确条款保障权益' },
  { step: '6', title: '项目交付', desc: '全程跟进确保顺利' }
]

const stats = [
  { number: '50+', label: '合作供应商' },
  { number: '100+', label: '成功案例' },
  { number: '24h', label: '快速响应' },
  { number: '95%', label: '客户满意度' }
]

const formData = ref({ name: '', email: '', message: '' })

const handleSubmit = () => {
  alert(`感谢咨询！\n姓名：${formData.value.name}\n邮箱：${formData.value.email}`)
  formData.value = { name: '', email: '', message: '' }
}

const scrollTo = (section) => {
  activeSection.value = section
  document.getElementById(section)?.scrollIntoView({ behavior: 'smooth' })
}

onMounted(() => {
  window.addEventListener('scroll', () => {
    const sections = ['home', 'services', 'advantages', 'process', 'contact']
    for (const section of sections) {
      const el = document.getElementById(section)
      if (el) {
        const rect = el.getBoundingClientRect()
        if (rect.top <= 150 && rect.bottom >= 150) {
          activeSection.value = section
          break
        }
      }
    }
  })
})
</script>

<template>
  <div class="app">
    <!-- Navigation -->
    <nav class="navbar" :class="{ scrolled: activeSection !== 'home' }">
      <div class="container nav-container">
        <a href="#" class="logo">
          <div class="logo-icon">CP</div>
          <span>PowerBroker</span>
        </a>
        <ul class="nav-links">
          <li :class="{ active: activeSection === 'home' }"><a @click.prevent="scrollTo('home')">首页</a></li>
          <li :class="{ active: activeSection === 'services' }"><a @click.prevent="scrollTo('services')">服务</a></li>
          <li :class="{ active: activeSection === 'advantages' }"><a @click.prevent="scrollTo('advantages')">优势</a></li>
          <li :class="{ active: activeSection === 'process' }"><a @click.prevent="scrollTo('process')">流程</a></li>
          <li><a @click.prevent="scrollTo('contact')" class="cta-btn">立即咨询</a></li>
        </ul>
      </div>
    </nav>

    <!-- Hero -->
    <section id="home" class="hero">
      <div class="hero-bg"></div>
      <div class="container hero-content">
        <div class="hero-badge">专业算力中介服务</div>
        <h1>算力资源<span>出海中介服务</span></h1>
        <p class="hero-subtitle">连接全球算力供需双方，让算力跨境更简单</p>
        <div class="hero-buttons">
          <a @click.prevent="scrollTo('contact')" class="btn btn-primary">立即咨询 →</a>
          <a @click.prevent="scrollTo('services')" class="btn btn-secondary">了解更多</a>
        </div>
      </div>
    </section>

    <!-- Stats -->
    <section class="stats">
      <div class="container stats-grid">
        <div v-for="stat in stats" :key="stat.label" class="stat-item">
          <div class="stat-number">{{ stat.number }}</div>
          <div class="stat-label">{{ stat.label }}</div>
        </div>
      </div>
    </section>

    <!-- Services -->
    <section id="services" class="services">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">我们的服务</span>
          <h2>一站式算力中介服务</h2>
          <p>从需求对接到方案落地，我们为您提供全流程专业服务</p>
        </div>
        <div class="services-grid">
          <div v-for="service in services" :key="service.title" class="service-card">
            <div class="service-icon">{{ service.icon }}</div>
            <h3>{{ service.title }}</h3>
            <p>{{ service.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Advantages -->
    <section id="advantages" class="advantages">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">核心优势</span>
          <h2>为什么选择我们</h2>
          <p>专业团队为您提供最优质的算力中介服务</p>
        </div>
        <div class="advantages-grid">
          <div v-for="adv in advantages" :key="adv.title" class="advantage-card">
            <div class="advantage-icon">{{ adv.icon }}</div>
            <h3>{{ adv.title }}</h3>
            <p>{{ adv.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Process -->
    <section id="process" class="process">
      <div class="container">
        <div class="section-header">
          <span class="section-tag">服务流程</span>
          <h2>简单六步完成合作</h2>
          <p>规范流程确保每一步都清晰可控</p>
        </div>
        <div class="process-steps">
          <div v-for="p in process" :key="p.step" class="process-step">
            <div class="step-number">{{ p.step }}</div>
            <h4>{{ p.title }}</h4>
            <p>{{ p.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact -->
    <section id="contact" class="contact">
      <div class="contact-bg"></div>
      <div class="container contact-content">
        <div class="contact-info">
          <h2>立即联系我们</h2>
          <p>准备好开启您的算力出海之旅了吗？我们随时为您提供专业咨询。</p>
          <div class="contact-methods">
            <div class="contact-method">
              <div class="contact-icon">📧</div>
              <span>contact@powerbroker.com</span>
            </div>
            <div class="contact-method">
              <div class="contact-icon">💬</div>
              <span>微信：扫码添加</span>
            </div>
          </div>
        </div>
        <form class="contact-form" @submit.prevent="handleSubmit">
          <div class="form-group">
            <label>姓名 / Name</label>
            <input v-model="formData.name" type="text" placeholder="请输入您的姓名" required>
          </div>
          <div class="form-group">
            <label>邮箱 / Email</label>
            <input v-model="formData.email" type="email" placeholder="your@email.com" required>
          </div>
          <div class="form-group">
            <label>需求描述 / Message</label>
            <textarea v-model="formData.message" placeholder="请描述您的算力需求..." required></textarea>
          </div>
          <button type="submit" class="form-submit">提交咨询</button>
        </form>
      </div>
    </section>

    <!-- Footer -->
    <footer>
      <div class="container">
        <p>© 2026 PowerBroker. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --primary: #0066FF;
  --primary-dark: #0052CC;
  --primary-light: #E6F0FF;
  --accent: #FF6B35;
  --accent-hover: #E55A2B;
  --dark: #1A1A2E;
  --gray-900: #111827;
  --gray-700: #374151;
  --gray-500: #6B7280;
  --gray-100: #F3F4F6;
  --white: #FFFFFF;
}

body {
  font-family: 'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif;
  color: var(--gray-900);
  line-height: 1.6;
  background: var(--white);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

/* Navbar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 16px 0;
  transition: all 0.3s;
}

.navbar.scrolled {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  box-shadow: 0 1px 0 rgba(0, 0, 0, 0.05);
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 20px;
  font-weight: 700;
  color: var(--primary);
  text-decoration: none;
}

.logo-icon {
  width: 36px;
  height: 36px;
  background: linear-gradient(135deg, var(--primary), var(--primary-dark));
  border-radius: 8px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: 700;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 32px;
  list-style: none;
}

.nav-links a {
  color: var(--gray-700);
  text-decoration: none;
  font-weight: 500;
  font-size: 15px;
  cursor: pointer;
  transition: color 0.2s;
}

.nav-links a:hover,
.nav-links li.active a {
  color: var(--primary);
}

.cta-btn {
  background: var(--primary);
  color: white !important;
  padding: 10px 20px;
  border-radius: 8px;
}

.cta-btn:hover {
  background: var(--primary-dark);
}

/* Hero */
.hero {
  padding: 180px 0 120px;
  position: relative;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(135deg, #0A0A1A 0%, #1A1A2E 50%, #16213E 100%);
}

.hero-bg::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 20% 50%, rgba(0, 102, 255, 0.15) 0%, transparent 50%),
    radial-gradient(circle at 80% 20%, rgba(0, 102, 255, 0.1) 0%, transparent 40%);
}

.hero-content {
  position: relative;
  z-index: 1;
  text-align: center;
}

.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(0, 102, 255, 0.15);
  border: 1px solid rgba(0, 102, 255, 0.3);
  padding: 8px 16px;
  border-radius: 100px;
  font-size: 14px;
  color: #60A5FA;
  margin-bottom: 24px;
}

.hero h1 {
  font-size: clamp(36px, 6vw, 64px);
  font-weight: 700;
  color: white;
  line-height: 1.2;
  margin-bottom: 24px;
}

.hero h1 span {
  background: linear-gradient(135deg, #60A5FA, #0066FF);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.hero-subtitle {
  font-size: clamp(18px, 2.5vw, 22px);
  color: rgba(255, 255, 255, 0.7);
  max-width: 640px;
  margin: 0 auto 40px;
}

.hero-buttons {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 16px 32px;
  border-radius: 12px;
  font-size: 16px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.3s;
  cursor: pointer;
  border: none;
}

.btn-primary {
  background: var(--accent);
  color: white;
}

.btn-primary:hover {
  background: var(--accent-hover);
  transform: translateY(-2px);
}

.btn-secondary {
  background: rgba(255, 255, 255, 0.1);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.btn-secondary:hover {
  background: rgba(255, 255, 255, 0.15);
}

/* Stats */
.stats {
  padding: 60px 0;
  background: var(--white);
  border-bottom: 1px solid var(--gray-100);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 32px;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 40px;
  font-weight: 700;
  color: var(--primary);
}

.stat-label {
  font-size: 14px;
  color: var(--gray-500);
}

/* Services */
.services {
  padding: 100px 0;
  background: var(--gray-100);
}

.section-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-tag {
  display: inline-block;
  background: var(--primary-light);
  color: var(--primary);
  padding: 6px 16px;
  border-radius: 100px;
  font-size: 14px;
  font-weight: 600;
  margin-bottom: 16px;
}

.section-header h2 {
  font-size: clamp(28px, 4vw, 40px);
  font-weight: 700;
  margin-bottom: 16px;
}

.section-header p {
  font-size: 18px;
  color: var(--gray-500);
  max-width: 600px;
  margin: 0 auto;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 24px;
}

.service-card {
  background: white;
  border-radius: 16px;
  padding: 32px;
  transition: all 0.3s;
}

.service-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.08);
}

.service-icon {
  font-size: 40px;
  margin-bottom: 16px;
}

.service-card h3 {
  font-size: 20px;
  font-weight: 600;
  margin-bottom: 12px;
}

.service-card p {
  color: var(--gray-500);
}

/* Advantages */
.advantages {
  padding: 100px 0;
  background: white;
}

.advantages-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 32px;
}

.advantage-card {
  text-align: center;
  padding: 40px 24px;
  border-radius: 16px;
  transition: all 0.3s;
}

.advantage-card:hover {
  background: var(--gray-100);
}

.advantage-icon {
  width: 72px;
  height: 72px;
  background: linear-gradient(135deg, var(--primary), var(--primary-dark));
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 20px;
  font-size: 32px;
}

.advantage-card h3 {
  font-size: 18px;
  font-weight: 600;
  margin-bottom: 8px;
}

.advantage-card p {
  font-size: 14px;
  color: var(--gray-500);
}

/* Process */
.process {
  padding: 100px 0;
  background: linear-gradient(180deg, var(--gray-100) 0%, white 100%);
}

.process-steps {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 16px;
}

.process-step {
  text-align: center;
  position: relative;
}

.process-step:not(:last-child)::after {
  content: '';
  position: absolute;
  top: 28px;
  right: -50%;
  width: 100%;
  height: 2px;
  background: linear-gradient(90deg, var(--primary), var(--primary-light));
}

.step-number {
  width: 56px;
  height: 56px;
  background: var(--primary);
  color: white;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  font-weight: 700;
  margin: 0 auto 16px;
}

.process-step h4 {
  font-size: 15px;
  font-weight: 600;
  margin-bottom: 8px;
}

.process-step p {
  font-size: 13px;
  color: var(--gray-500);
}

/* Contact */
.contact {
  padding: 100px 0;
  position: relative;
  overflow: hidden;
}

.contact-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: var(--dark);
}

.contact-bg::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: 
    radial-gradient(circle at 30% 30%, rgba(0, 102, 255, 0.2) 0%, transparent 50%),
    radial-gradient(circle at 70% 70%, rgba(255, 107, 53, 0.1) 0%, transparent 50%);
}

.contact-content {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 60px;
  align-items: center;
}

.contact-info h2 {
  font-size: clamp(28px, 4vw, 40px);
  font-weight: 700;
  color: white;
  margin-bottom: 20px;
}

.contact-info p {
  font-size: 18px;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 32px;
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 16px;
  color: white;
  font-size: 16px;
}

.contact-icon {
  width: 48px;
  height: 48px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
}

.contact-form {
  background: white;
  border-radius: 20px;
  padding: 40px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  font-size: 14px;
  font-weight: 600;
  color: var(--gray-700);
  margin-bottom: 8px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 14px 16px;
  border: 1px solid var(--gray-100);
  border-radius: 10px;
  font-size: 15px;
  font-family: inherit;
  transition: all 0.2s;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--primary);
  box-shadow: 0 0 0 3px var(--primary-light);
}

.form-group textarea {
  min-height: 120px;
  resize: vertical;
}

.form-submit {
  width: 100%;
  padding: 16px;
  background: var(--accent);
  color: white;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s;
}

.form-submit:hover {
  background: var(--accent-hover);
}

/* Footer */
footer {
  padding: 40px 0;
  background: var(--gray-900);
  text-align: center;
}

footer p {
  color: rgba(255, 255, 255, 0.5);
  font-size: 14px;
}

/* Responsive */
@media (max-width: 1024px) {
  .process-steps {
    grid-template-columns: repeat(3, 1fr);
    gap: 40px 20px;
  }
  .process-step:not(:last-child)::after {
    display: none;
  }
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
  }
  .hero {
    padding: 140px 0 80px;
  }
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .contact-content {
    grid-template-columns: 1fr;
  }
  .process-steps {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .hero-buttons {
    flex-direction: column;
  }
  .btn {
    width: 100%;
    justify-content: center;
  }
}
</style>
