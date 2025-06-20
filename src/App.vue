<template>
  <div id="app">
    <!-- Header -->
    <header class="header">
      <div class="container">
        <div class="header-content">
          <div class="logo">
            <q-icon name="euro" size="32px" color="primary" />
            <span class="logo-text">MoneyInput</span>
          </div>
          <nav class="nav">
            <a href="#features" class="nav-link">Características</a>
            <a href="#demo" class="nav-link">Demo</a>
            <a href="#installation" class="nav-link">Instalación</a>
            <a href="#examples" class="nav-link">Ejemplos</a>
          </nav>
        </div>
      </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
      <div class="container">
        <div class="hero-content">
          <h1 class="hero-title">MoneyInput</h1>
          <p class="hero-subtitle">
            Componente de entrada monetaria para Vue.js + Quasar<br>
            Formato español: <strong>1.234,56 €</strong>
          </p>
          <div class="hero-demo">
            <money-input v-model="heroValue" label="Pruébalo aquí" hint="Introduce un valor monetario" :outlined="true"
              :filled="false" color="primary" size="lg" />
            <div class="hero-value">
              Valor: <code>{{ heroValue }}</code> ({{ typeof heroValue }})
            </div>
          </div>
          <div class="hero-buttons">
            <q-btn color="primary" size="lg" label="Ver Demo Completa" @click="scrollTo('#demo')" unelevated rounded
              class="hero-btn-primary" />
            <q-btn outline color="white" size="lg" label="GitHub" icon="fab fa-github" @click="openGitHub" rounded
              class="hero-btn-secondary" />
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features">
      <div class="container">
        <h2 class="section-title">Características Principales</h2>
        <div class="features-grid">
          <div class="feature-card">
            <q-icon name="language" size="48px" color="primary" />
            <h3>Formato Español</h3>
            <p>Visualización automática en formato español (1.234,56 €) mientras mantiene el valor numérico interno</p>
          </div>
          <div class="feature-card">
            <q-icon name="content_paste" size="48px" color="primary" />
            <h3>Múltiples Formatos</h3>
            <p>Soporte para copiar/pegar desde múltiples formatos: 1234, 1234.56, 1.234,56 €</p>
          </div>
          <div class="feature-card">
            <q-icon name="verified" size="48px" color="primary" />
            <h3>Validaciones Integradas</h3>
            <p>Validaciones built-in: obligatorio, numérico, min/max, y reglas personalizadas</p>
          </div>
          <div class="feature-card">
            <q-icon name="palette" size="48px" color="primary" />
            <h3>Estilos Quasar</h3>
            <p>Todos los estilos y atributos de q-input: outlined, filled, dense, colors, etc.</p>
          </div>
          <div class="feature-card">
            <q-icon name="integration_instructions" size="48px" color="primary" />
            <h3>Fácil Integración</h3>
            <p>Compatible con v-model, reactive, y todas las características de Vue 3</p>
          </div>
          <div class="feature-card">
            <q-icon name="smartphone" size="48px" color="primary" />
            <h3>Responsive</h3>
            <p>Funciona perfectamente en desktop, tablet y móvil</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Demo Section -->
    <section id="demo" class="demo-section">
      <div class="container">
        <h2 class="section-title">Demo Interactiva</h2>
        <money-input-demo />
      </div>
    </section>

    <!-- Installation Section -->
    <section id="installation" class="installation">
      <div class="container">
        <h2 class="section-title">Instalación y Uso</h2>

        <div class="installation-content">
          <div class="step">
            <h3>1. Instalación</h3>
            <div class="code-block">
              <pre><code>npm install quasar vue
# o
yarn add quasar vue</code></pre>
            </div>
          </div>

          <div class="step">
            <h3>2. Importar el Componente</h3>
            <div class="code-block">
              <pre><code>import MoneyInput from './components/MoneyInput.vue'</code></pre>
            </div>
          </div>

          <div class="step">
            <h3>3. Uso Básico</h3>
            <div class="code-block">
              <pre><code>&lt;template&gt;
  &lt;money-input
    v-model="amount"
    label="Importe"
    :required="true"
  /&gt;
&lt;/template&gt;

&lt;script setup&gt;
import { ref } from 'vue'
import MoneyInput from './components/MoneyInput.vue'

const amount = ref(null)
&lt;/script&gt;</code></pre>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Examples Section -->
    <section id="examples" class="examples">
      <div class="container">
        <h2 class="section-title">Ejemplos de Uso</h2>

        <div class="examples-grid">
          <div class="example-card">
            <h3>Básico</h3>
            <money-input v-model="example1" label="Campo básico" />
            <div class="example-code">
              <pre><code>&lt;money-input v-model="amount" label="Campo básico" /&gt;</code></pre>
            </div>
          </div>

          <div class="example-card">
            <h3>Con Validaciones</h3>
            <money-input v-model="example2" label="Con límites" :required="true" :min="10" :max="1000"
              hint="Entre 10€ y 1000€" />
            <div class="example-code">
              <pre><code>&lt;money-input
  v-model="amount"
  label="Con límites"
  :required="true"
  :min="10"
  :max="1000"
/&gt;</code></pre>
            </div>
          </div>

          <div class="example-card">
            <h3>Outlined Style</h3>
            <money-input v-model="example3" label="Estilo outlined" :outlined="true" :filled="false"
              color="secondary" />
            <div class="example-code">
              <pre><code>&lt;money-input
  v-model="amount"
  label="Estilo outlined"
  :outlined="true"
  :filled="false"
  color="secondary"
/&gt;</code></pre>
            </div>
          </div>

          <div class="example-card">
            <h3>Con Validación Personalizada</h3>
            <money-input v-model="example4" label="Múltiplos de 50" :required="true" :custom-rules="[multipleOf50]"
              hint="Debe ser múltiplo de 50" />
            <div class="example-code">
              <pre><code>const multipleOf50 = (val) => {
  if (!val) return true
  const num = parseFloat(val)
  return num % 50 === 0 || 'Debe ser múltiplo de 50'
}

&lt;money-input
  v-model="amount"
  :custom-rules="[multipleOf50]"
/&gt;</code></pre>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-left">
            <div class="logo">
              <q-icon name="euro" size="24px" color="primary" />
              <span class="logo-text">MoneyInput</span>
            </div>
            <p>Componente de entrada monetaria para Vue.js + Quasar</p>
          </div>
          <div class="footer-right">
            <p>Desarrollado con ❤️ por <strong>Sistemas Snackson</strong></p>
            <p>© 2024 - Todos los derechos reservados</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import {ref} from 'vue'
import MoneyInput from './components/MoneyInput.vue'
import MoneyInputDemo from './pages/MoneyInputDemo.vue'

// Variables reactivas para ejemplos
const heroValue = ref(1234.56)
const example1 = ref(null)
const example2 = ref(50)
const example3 = ref(null)
const example4 = ref(null)

// Regla de validación personalizada
const multipleOf50 = (val) => {
  if (!val) return true
  const num = parseFloat(val.toString().replace(/[^\d.,]/g, '').replace(',', '.'))
  return num % 50 === 0 || 'Debe ser múltiplo de 50'
}

// Métodos
const scrollTo = (selector) => {
  const element = document.querySelector(selector)
  if (element) {
    element.scrollIntoView({behavior: 'smooth'})
  }
}

const openGitHub = () => {
  // Aquí puedes poner tu URL de GitHub
  window.open('https://github.com/tu-usuario/money-input', '_blank')
}
</script>

<style scoped>
/* Variables CSS */
:root {
  --primary-color: #1976d2;
  --primary-dark: #1565c0;
  --secondary-color: #424242;
  --accent-color: #ff4081;
  --accent-light: #ff80ab;
  --background-color: #f8fafc;
  --background-gradient: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  --text-color: #1a202c;
  --text-secondary: #718096;
  --border-color: #e2e8f0;
  --card-shadow: 0 10px 25px rgba(0, 0, 0, 0.08);
  --card-shadow-hover: 0 20px 40px rgba(0, 0, 0, 0.12);
}

/* Reset y base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Roboto', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  color: var(--text-color);
  line-height: 1.7;
  overflow-x: hidden;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Header */
.header {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(20px);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  transition: all 0.3s ease;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;
}

.logo {
  display: flex;
  align-items: center;
  gap: 12px;
  transition: transform 0.3s ease;
}

.logo:hover {
  transform: scale(1.05);
}

.logo-text {
  font-size: 26px;
  font-weight: 700;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.nav {
  display: flex;
  gap: 32px;
}

.nav-link {
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  position: relative;
  transition: all 0.3s ease;
  padding: 8px 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: var(--primary-color);
  transform: translateY(-2px);
}

.nav-link:hover::after {
  width: 100%;
}

/* Hero Section */
.hero {
  background: var(--background-gradient);
  color: white;
  padding: 140px 0 100px;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Ccircle cx='30' cy='30' r='2'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
  animation: float 20s infinite linear;
}

@keyframes float {
  0% {
    transform: translateY(0px);
  }

  100% {
    transform: translateY(-60px);
  }
}

.hero-title {
  font-size: 4.5rem;
  font-weight: 200;
  margin-bottom: 24px;
  letter-spacing: -2px;
  animation: fadeInUp 1s ease-out;
}

.hero-subtitle {
  font-size: 1.4rem;
  margin-bottom: 50px;
  opacity: 0.95;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
  line-height: 1.6;
  animation: fadeInUp 1s ease-out 0.2s both;
}

.hero-demo {
  max-width: 450px;
  margin: 0 auto 50px;
  background: rgba(255, 255, 255, 0.15);
  padding: 40px;
  border-radius: 24px;
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: all 0.3s ease;
  animation: fadeInUp 1s ease-out 0.4s both;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.hero-demo:hover {
  transform: translateY(-5px);
  box-shadow: 0 15px 45px rgba(0, 0, 0, 0.15);
}

.hero-value {
  margin-top: 20px;
  font-size: 15px;
  opacity: 0.9;
  font-weight: 500;
}

.hero-value code {
  background: rgba(255, 255, 255, 0.25);
  padding: 6px 12px;
  border-radius: 8px;
  font-family: 'Monaco', 'Consolas', monospace;
  font-weight: 600;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.hero-buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
  animation: fadeInUp 1s ease-out 0.6s both;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Sections */
.section-title {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 60px;
  color: var(--text-color);
  font-weight: 300;
}

/* Features Section */
.features {
  padding: 100px 0;
  background: white;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 50px;
}

.feature-card {
  text-align: center;
  padding: 50px 30px;
  border-radius: 20px;
  background: white;
  box-shadow: var(--card-shadow);
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  border: 1px solid var(--border-color);
  position: relative;
  overflow: hidden;
}

.feature-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.feature-card:hover {
  transform: translateY(-12px) scale(1.02);
  box-shadow: var(--card-shadow-hover);
}

.feature-card:hover::before {
  transform: scaleX(1);
}

.feature-card h3 {
  font-size: 1.5rem;
  margin: 25px 0 20px;
  color: var(--text-color);
  font-weight: 600;
}

.feature-card p {
  color: var(--text-secondary);
  line-height: 1.7;
  font-size: 1rem;
}

/* Demo Section */
.demo-section {
  padding: 80px 0;
  background: var(--background-color);
}

/* Installation Section */
.installation {
  padding: 80px 0;
  background: white;
}

.installation-content {
  max-width: 800px;
  margin: 0 auto;
}

.step {
  margin-bottom: 40px;
}

.step h3 {
  font-size: 1.5rem;
  margin-bottom: 16px;
  color: var(--primary-color);
}

.code-block {
  background: #2d3748;
  border-radius: 8px;
  overflow: hidden;
}

.code-block pre {
  padding: 20px;
  margin: 0;
  overflow-x: auto;
}

.code-block code {
  color: #e2e8f0;
  font-family: 'Monaco', 'Consolas', monospace;
  font-size: 14px;
  line-height: 1.5;
}

/* Examples Section */
.examples {
  padding: 80px 0;
  background: var(--background-color);
}

.examples-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 32px;
}

.example-card {
  background: white;
  padding: 40px;
  border-radius: 20px;
  box-shadow: var(--card-shadow);
  transition: all 0.3s ease;
  border: 1px solid var(--border-color);
  position: relative;
  overflow: hidden;
}

.example-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.example-card:hover {
  transform: translateY(-8px);
  box-shadow: var(--card-shadow-hover);
}

.example-card:hover::before {
  transform: scaleX(1);
}

.example-card h3 {
  font-size: 1.3rem;
  margin-bottom: 20px;
  color: var(--text-color);
}

.example-code {
  margin-top: 20px;
  background: #f8f9fa;
  border-radius: 8px;
  overflow: hidden;
}

.example-code pre {
  padding: 16px;
  margin: 0;
  overflow-x: auto;
}

.example-code code {
  font-family: 'Monaco', 'Consolas', monospace;
  font-size: 12px;
  line-height: 1.4;
  color: #2d3748;
}

/* Footer */
.footer {
  background: #2d3748;
  color: white;
  padding: 40px 0;
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}

.footer-left .logo-text {
  color: white;
}

.footer-right {
  text-align: right;
}

.footer-right p {
  margin: 4px 0;
  opacity: 0.8;
}

/* Responsive */
@media (max-width: 768px) {
  .nav {
    display: none;
  }

  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.1rem;
  }

  .hero-buttons {
    flex-direction: column;
    align-items: center;
  }

  .features-grid {
    grid-template-columns: 1fr;
  }

  .examples-grid {
    grid-template-columns: 1fr;
  }

  .footer-content {
    flex-direction: column;
    text-align: center;
  }

  .footer-right {
    text-align: center;
  }
}

/* Smooth scroll */
html {
  scroll-behavior: smooth;
}

/* Mejoras adicionales */
.hero-btn-primary {
  background: linear-gradient(135deg, var(--primary-color), var(--primary-dark)) !important;
  box-shadow: 0 8px 25px rgba(25, 118, 210, 0.3) !important;
  transition: all 0.3s ease !important;
}

.hero-btn-primary:hover {
  transform: translateY(-3px) !important;
  box-shadow: 0 12px 35px rgba(25, 118, 210, 0.4) !important;
}

.hero-btn-secondary {
  backdrop-filter: blur(10px) !important;
  border: 2px solid rgba(255, 255, 255, 0.3) !important;
  transition: all 0.3s ease !important;
}

.hero-btn-secondary:hover {
  background: rgba(255, 255, 255, 0.1) !important;
  transform: translateY(-3px) !important;
  border-color: rgba(255, 255, 255, 0.5) !important;
}

/* Animación de scroll reveal */
@keyframes slideInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }

  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideInRight {
  from {
    opacity: 0;
    transform: translateX(50px);
  }

  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* Mejora para el footer */
.footer {
  background: linear-gradient(135deg, #2d3748 0%, #1a202c 100%);
}

.footer-content {
  animation: slideInLeft 1s ease-out;
}

/* Estilos para el código */
.code-block {
  position: relative;
}

.code-block::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 2px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
}

/* Mejora para las secciones */
.section-title {
  position: relative;
  display: inline-block;
}

.section-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: linear-gradient(135deg, var(--primary-color), var(--accent-color));
  border-radius: 2px;
}
</style>
