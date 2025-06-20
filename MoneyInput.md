# MoneyInput Component

Componente de input monetario para Quasar Vue.js que permite la entrada de valores numéricos con formato español y devuelve valores en formato internacional.

## Características principales

- ✅ **Formato de visualización español**: 1.234,56 €
- ✅ **Valor v-model internacional**: 1234.56
- ✅ **Soporte multi-formato**: Acepta pegado en formatos 1234, 1234.83, 123.455,09
- ✅ **Validaciones integradas**: Obligatorio, numérico, min/max
- ✅ **Estados**: disable, readonly
- ✅ **Validaciones personalizadas**: Soporte para rules custom

## Uso básico

```vue
<template>
  <money-input v-model="precio" label="Precio" />
</template>

<script setup>
import { ref } from 'vue'
import MoneyInput from '@/components/MoneyInput.vue'

const precio = ref(null)
</script>
```

## Props

| Prop           | Tipo                   | Defecto                 | Descripción                         |
| -------------- | ---------------------- | ----------------------- | ----------------------------------- |
| `modelValue`   | `Number\|String\|null` | `null`                  | Valor del input (v-model)           |
| `label`        | `String`               | `'Importe'`             | Etiqueta del campo                  |
| `hint`         | `String`               | `'Formato: 1.234,56 €'` | Texto de ayuda                      |
| `placeholder`  | `String`               | `'0,00'`                | Placeholder del input               |
| `required`     | `Boolean`              | `false`                 | Campo obligatorio                   |
| `numeric`      | `Boolean`              | `true`                  | Validación numérica                 |
| `disable`      | `Boolean`              | `false`                 | Campo deshabilitado                 |
| `readonly`     | `Boolean`              | `false`                 | Campo de solo lectura               |
| `min`          | `Number`               | `null`                  | Valor mínimo permitido              |
| `max`          | `Number`               | `null`                  | Valor máximo permitido              |
| `decimals`     | `Number`               | `2`                     | Número de decimales a mostrar       |
| `customRules`  | `Array`                | `[]`                    | Reglas de validación personalizadas |
| `errorMessage` | `String`               | `''`                    | Mensaje de error personalizado      |
| `hasError`     | `Boolean`              | `false`                 | Estado de error externo             |

### Props de diseño de Quasar

| Prop         | Tipo              | Defecto | Descripción                    |
| ------------ | ----------------- | ------- | ------------------------------ |
| `filled`     | `Boolean`         | `true`  | Diseño filled (relleno)        |
| `outlined`   | `Boolean`         | `false` | Diseño outlined (contorno)     |
| `standout`   | `Boolean\|String` | `false` | Diseño standout (destacado)    |
| `borderless` | `Boolean`         | `false` | Diseño borderless (sin bordes) |

### Props adicionales de Quasar

| Prop         | Tipo             | Defecto     | Descripción                      |
| ------------ | ---------------- | ----------- | -------------------------------- |
| `dense`      | `Boolean`        | `false`     | Versión compacta del componente  |
| `rounded`    | `Boolean`        | `false`     | Bordes redondeados               |
| `square`     | `Boolean`        | `false`     | Bordes cuadrados (sin redondear) |
| `clearable`  | `Boolean`        | `false`     | Mostrar icono para limpiar       |
| `clearIcon`  | `String`         | `'cancel'`  | Icono del botón limpiar          |
| `loading`    | `Boolean`        | `false`     | Estado de carga                  |
| `dark`       | `Boolean`        | `false`     | Modo oscuro                      |
| `color`      | `String`         | `'primary'` | Color del componente             |
| `bgColor`    | `String`         | `undefined` | Color de fondo                   |
| `labelColor` | `String`         | `undefined` | Color de la etiqueta             |
| `size`       | `String`         | `undefined` | Tamaño del input                 |
| `debounce`   | `String\|Number` | `0`         | Tiempo de debounce en ms         |

## Eventos

| Evento              | Descripción                               |
| ------------------- | ----------------------------------------- |
| `update:modelValue` | Se emite cuando cambia el valor (v-model) |

## Métodos expuestos

| Método              | Descripción                     |
| ------------------- | ------------------------------- |
| `validate()`        | Ejecuta la validación del campo |
| `resetValidation()` | Resetea la validación           |
| `focus()`           | Da foco al campo                |
| `blur()`            | Quita el foco del campo         |

## Ejemplos de uso

### Campo básico

```vue
<money-input v-model="importe" label="Importe" />
```

### Campo obligatorio con límites

```vue
<money-input
  v-model="precio"
  label="Precio"
  :required="true"
  :min="0"
  :max="9999"
  hint="Entre 0€ y 9999€"
/>
```

### Campo con validaciones personalizadas

```vue
<money-input v-model="descuento" label="Descuento" :custom-rules="[multipleOf10Rule]" />

<script setup>
const multipleOf10Rule = (val) => {
  if (!val) return true
  const num = parseFloat(val.toString().replace(',', '.'))
  return num % 10 === 0 || 'Debe ser múltiplo de 10'
}
</script>
```

### Campo deshabilitado

```vue
<money-input v-model="total" label="Total calculado" :disable="true" />
```

### Diferentes diseños de Quasar

```vue
<!-- Diseño filled (por defecto) -->
<money-input v-model="precio1" label="Filled (defecto)" />

<!-- Diseño outlined -->
<money-input v-model="precio2" label="Outlined" :filled="false" :outlined="true" />

<!-- Diseño standout -->
<money-input v-model="precio3" label="Standout" :filled="false" :standout="true" />

<!-- Diseño borderless -->
<money-input v-model="precio4" label="Borderless" :filled="false" :borderless="true" />
```

### Con atributos adicionales

```vue
<!-- Versión compacta con color personalizado -->
<money-input
  v-model="precio"
  label="Precio compacto"
  :dense="true"
  color="secondary"
  :clearable="true"
/>

<!-- Con bordes redondeados y debounce -->
<money-input
  v-model="importe"
  label="Importe con debounce"
  :outlined="true"
  :filled="false"
  :rounded="true"
  :debounce="500"
/>

<!-- En modo oscuro con loading -->
<money-input
  v-model="total"
  label="Total en modo oscuro"
  :dark="true"
  :loading="isCalculating"
  color="amber"
/>
```

## Formatos soportados para copiar/pegar

El componente reconoce automáticamente estos formatos al pegar:

- `1234` → 1234.00
- `1234.83` → 1234.83 (formato decimal internacional)
- `1234,83` → 1234.83 (formato decimal español)
- `123.455,09` → 123455.09 (formato español con separador de miles)
- `12.345.678,99` → 12345678.99 (formato español completo)
- `1.234.567` → 1234567 (separador de miles sin decimales)

### Lógica de detección de formatos:

- **Punto + Coma**: Formato español (punto=miles, coma=decimal)
- **Solo Coma**: Formato decimal español si 1-2 dígitos después
- **Solo Punto**:
  - Formato decimal si 1-2 dígitos después del punto
  - Para 3 dígitos: decimal si parte entera < 4 dígitos, miles si >= 4 dígitos
  - Más de 3 dígitos: separador de miles

## Comportamiento del formato

### Visualización

- **En reposo**: Formato español con separadores de miles: `12.345,67 €`
- **Durante edición**: Formato simplificado para facilitar la entrada: `12345.67`
- **Al perder foco**: Vuelve al formato español

### V-model

- Siempre devuelve el valor en formato de número flotante internacional
- `null` cuando el campo está vacío
- `Number` cuando tiene un valor válido

## Validaciones incluidas

### Validación automática

- **required**: Verifica que el campo no esté vacío
- **numeric**: Verifica que sea un número válido
- **min/max**: Verifica que esté dentro del rango especificado

### Mensajes de error

- "Este campo es obligatorio"
- "Debe ser un número válido"
- "El valor mínimo es X"
- "El valor máximo es X"

## Consideraciones técnicas

- Usa `Intl.NumberFormat` para el formato español
- Maneja automáticamente la conversión entre formatos
- Compatible con todas las props estándar de QInput
- Basado en el componente QInput de Quasar
- Soporte completo para validaciones reactivas

## Dependencias

- Vue 3
- Quasar Framework
- QInput component
