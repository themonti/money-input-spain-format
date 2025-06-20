# 💰 MoneyInput

Componente de entrada monetaria para **Vue.js + Quasar** con formato español automático.

[![Demo en Vercel](https://img.shields.io/badge/Demo-Vercel-000000?style=for-the-badge&logo=vercel)](https://tu-url-vercel.vercel.app)
[![Vue 3](https://img.shields.io/badge/Vue-3-4FC08D?style=for-the-badge&logo=vue.js)](https://vuejs.org/)
[![Quasar](https://img.shields.io/badge/Quasar-2.16-1976D2?style=for-the-badge&logo=quasar)](https://quasar.dev/)

## ✨ Características

- 🇪🇸 **Formato español automático**: Muestra valores como `1.234,56 €`
- 📋 **Soporte multi-formato**: Pega desde `1234`, `1234.56`, `1.234,56 €`
- ✅ **Validaciones integradas**: Obligatorio, numérico, min/max, reglas personalizadas
- 🎨 **Estilos Quasar**: Todos los diseños (`outlined`, `filled`, `dense`, etc.)
- 📱 **Responsive**: Funciona en desktop, tablet y móvil
- ⚡ **Vue 3 + Composition API**: Totalmente compatible con v-model

## 🚀 Demo en Vivo

👉 **[Ver Demo Interactiva](https://tu-url-vercel.vercel.app)**

## 📦 Instalación

```bash
npm install quasar vue
# o
yarn add quasar vue
```

## 🔧 Uso Básico

```vue
<template>
  <money-input v-model="amount" label="Importe" :required="true" />
</template>

<script setup>
import { ref } from 'vue'
import MoneyInput from './components/MoneyInput.vue'

const amount = ref(null)
</script>
```

## 📚 Ejemplos

### Ejemplo Básico

```vue
<money-input v-model="amount" label="Campo básico" />
```

### Con Validaciones

```vue
<money-input
  v-model="amount"
  label="Con límites"
  :required="true"
  :min="10"
  :max="1000"
  hint="Entre 10€ y 1000€"
/>
```

### Estilos Personalizados

```vue
<money-input
  v-model="amount"
  label="Estilo outlined"
  :outlined="true"
  :filled="false"
  color="secondary"
/>
```

### Validación Personalizada

```vue
<money-input v-model="amount" label="Múltiplos de 50" :custom-rules="[multipleOf50]" />

<script setup>
const multipleOf50 = (val) => {
  if (!val) return true
  const num = parseFloat(val)
  return num % 50 === 0 || 'Debe ser múltiplo de 50'
}
</script>
```

## 🔧 Props

| Prop          | Tipo            | Defecto                 | Descripción                         |
| ------------- | --------------- | ----------------------- | ----------------------------------- |
| `modelValue`  | `Number/String` | `null`                  | Valor del campo (v-model)           |
| `label`       | `String`        | `"Importe"`             | Etiqueta del campo                  |
| `hint`        | `String`        | `"Formato: 1.234,56 €"` | Texto de ayuda                      |
| `required`    | `Boolean`       | `false`                 | Campo obligatorio                   |
| `min`         | `Number`        | `null`                  | Valor mínimo                        |
| `max`         | `Number`        | `null`                  | Valor máximo                        |
| `disable`     | `Boolean`       | `false`                 | Deshabilitar campo                  |
| `readonly`    | `Boolean`       | `false`                 | Solo lectura                        |
| `customRules` | `Array`         | `[]`                    | Reglas de validación personalizadas |

## 🎨 Estilos Quasar Soportados

Todos los estilos y atributos de `q-input`:

- `filled`, `outlined`, `standout`, `borderless`
- `dense`, `rounded`, `square`
- `clearable`, `loading`, `dark`
- `color`, `bg-color`, `label-color`

## 💻 Desarrollo Local

```bash
# Instalar dependencias
npm install

# Servidor de desarrollo
npm run dev

# Build para producción
npm run build
```

## 🚀 Despliegue en Vercel

1. Haz fork de este repositorio
2. Conecta tu repositorio con Vercel
3. ¡Vercel detectará automáticamente la configuración!

## 🤝 Contribuir

Las contribuciones son bienvenidas. Por favor:

1. Haz fork del proyecto
2. Crea una rama para tu feature
3. Commit tus cambios
4. Push a la rama
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT - mira el archivo [LICENSE](LICENSE) para más detalles.

## 👨‍💻 Desarrollado por

**Sistemas Snackson** - [sistemas@snackson.com](mailto:sistemas@snackson.com)

---

⭐ Si te resulta útil, ¡danos una estrella en GitHub!
