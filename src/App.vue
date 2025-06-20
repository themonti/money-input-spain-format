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
            <q-btn color="primary" size="lg" label="Ver Demo Completa" @click="scrollTo('#demo')" unelevated />
            <q-btn outline color="primary" size="lg" label="GitHub" icon="fab fa-github" @click="openGitHub"
              class="q-ml-md" />
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
  --secondary-color: #424242;
  --accent-color: #ff4081;
  --background-color: #fafafa;
  --text-color: #212121;
  --text-secondary: #757575;
  --border-color: #e0e0e0;
}

/* Reset y base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Roboto', sans-serif;
  color: var(--text-color);
  line-height: 1.6;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

/* Header */
.header {
  background: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
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
  gap: 8px;
}

.logo-text {
  font-size: 24px;
  font-weight: 600;
  color: var(--primary-color);
}

.nav {
  display: flex;
  gap: 24px;
}

.nav-link {
  text-decoration: none;
  color: var(--text-color);
  font-weight: 500;
  transition: color 0.3s;
}

.nav-link:hover {
  color: var(--primary-color);
}

/* Hero Section */
.hero {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 140px 0 80px;
  text-align: center;
}

.hero-title {
  font-size: 4rem;
  font-weight: 300;
  margin-bottom: 16px;
}

.hero-subtitle {
  font-size: 1.3rem;
  margin-bottom: 40px;
  opacity: 0.9;
}

.hero-demo {
  max-width: 400px;
  margin: 0 auto 40px;
  background: rgba(255, 255, 255, 0.1);
  padding: 32px;
  border-radius: 16px;
  backdrop-filter: blur(10px);
}

.hero-value {
  margin-top: 16px;
  font-size: 14px;
  opacity: 0.8;
}

.hero-value code {
  background: rgba(255, 255, 255, 0.2);
  padding: 4px 8px;
  border-radius: 4px;
  font-family: 'Courier New', monospace;
}

.hero-buttons {
  display: flex;
  justify-content: center;
  gap: 16px;
  flex-wrap: wrap;
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
  padding: 80px 0;
  background: white;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 40px;
}

.feature-card {
  text-align: center;
  padding: 40px 24px;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  transition: transform 0.3s, box-shadow 0.3s;
}

.feature-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.12);
}

.feature-card h3 {
  font-size: 1.4rem;
  margin: 20px 0 16px;
  color: var(--text-color);
}

.feature-card p {
  color: var(--text-secondary);
  line-height: 1.6;
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
  padding: 32px;
  border-radius: 16px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
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
</style>
