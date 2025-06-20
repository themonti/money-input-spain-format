<template>
  <q-input
    ref="inputRef"
    v-model="displayValue"
    :rules="computedRules"
    :disable="disable"
    :readonly="readonly"
    :label="label"
    :hint="hint"
    :error="hasError"
    :error-message="errorMessage"
    :placeholder="placeholder"
    :filled="filled"
    :outlined="outlined"
    :standout="standout"
    :borderless="borderless"
    :dense="dense"
    :rounded="rounded"
    :square="square"
    :clearable="clearable"
    :clear-icon="clearIcon"
    :loading="loading"
    :dark="dark"
    :color="color"
    :bg-color="bgColor"
    :label-color="labelColor"
    :size="size"
    :debounce="debounce"
    suffix="€"
    @update:model-value="onInput"
    @paste="onPaste"
    @blur="onBlur"
    @focus="onFocus"
    input-class="text-right"
    v-bind="$attrs"
  >
    <template v-slot:prepend>
      <q-icon name="euro" />
    </template>
  </q-input>
</template>

<script setup>
  import { ref, computed, watch, nextTick } from "vue";

  // Props
  const props = defineProps({
    modelValue: {
      type: [Number, String],
      default: null,
    },
    label: {
      type: String,
      default: "Importe",
    },
    hint: {
      type: String,
      default: "Formato: 1.234,56 €",
    },
    placeholder: {
      type: String,
      default: "0,00",
    },
    required: {
      type: Boolean,
      default: false,
    },
    numeric: {
      type: Boolean,
      default: true,
    },
    disable: {
      type: Boolean,
      default: false,
    },
    readonly: {
      type: Boolean,
      default: false,
    },
    min: {
      type: Number,
      default: null,
    },
    max: {
      type: Number,
      default: null,
    },
    decimals: {
      type: Number,
      default: 2,
    },
    customRules: {
      type: Array,
      default: () => [],
    },
    errorMessage: {
      type: String,
      default: "",
    },
    hasError: {
      type: Boolean,
      default: false,
    },
    // Diseños de Quasar
    filled: {
      type: Boolean,
      default: true,
    },
    outlined: {
      type: Boolean,
      default: false,
    },
    standout: {
      type: [Boolean, String],
      default: false,
    },
    borderless: {
      type: Boolean,
      default: false,
    },
    // Atributos adicionales de Quasar
    dense: {
      type: Boolean,
      default: false,
    },
    rounded: {
      type: Boolean,
      default: false,
    },
    square: {
      type: Boolean,
      default: false,
    },
    clearable: {
      type: Boolean,
      default: false,
    },
    clearIcon: {
      type: String,
      default: "cancel",
    },
    loading: {
      type: Boolean,
      default: false,
    },
    dark: {
      type: Boolean,
      default: false,
    },
    color: {
      type: String,
      default: "primary",
    },
    bgColor: {
      type: String,
      default: undefined,
    },
    labelColor: {
      type: String,
      default: undefined,
    },
    size: {
      type: String,
      default: undefined,
    },
    debounce: {
      type: [String, Number],
      default: 0,
    },
  });

  // Emits
  const emit = defineEmits(["update:modelValue"]);

  // Refs
  const inputRef = ref(null);
  const displayValue = ref("");
  const isFocused = ref(false);

  // Función para formatear número a formato español
  const formatToSpanish = (value) => {
    if (value === null || value === undefined || value === "") return "";

    const num = typeof value === "string" ? parseFloat(value) : value;
    if (isNaN(num)) return "";

    return new Intl.NumberFormat("es-ES", {
      minimumFractionDigits: props.decimals,
      maximumFractionDigits: props.decimals,
    }).format(num);
  };

  // Función para parsear de formato español a internacional
  const parseFromSpanish = (value) => {
    if (!value || typeof value !== "string") return null;

    // Eliminar espacios y el símbolo €
    let cleanValue = value.replace(/\s/g, "").replace(/€/g, "");

    // Si está vacío, retornar null
    if (!cleanValue) return null;

    // Detectar el formato y convertir
    // Formato español: 123.456,78 o 1.234,56 o 1234,56
    // Formato internacional: 123456.78 o 1234.56

    // Si contiene tanto puntos como comas
    if (cleanValue.includes(".") && cleanValue.includes(",")) {
      // Es formato español: 123.456,78
      cleanValue = cleanValue.replace(/\./g, "").replace(",", ".");
    } else if (cleanValue.includes(",")) {
      // Solo tiene coma, verificar si es separador decimal o de miles
      const parts = cleanValue.split(",");
      if (parts.length === 2 && parts[1].length <= 2) {
        // Es separador decimal: 1234,56
        cleanValue = cleanValue.replace(",", ".");
      } else {
        // Es separador de miles: 1,234 (poco común en español)
        cleanValue = cleanValue.replace(/,/g, "");
      }
    } else if (cleanValue.includes(".")) {
      // Solo tiene punto, verificar contexto
      const parts = cleanValue.split(".");

      if (parts.length === 2) {
        // Dos partes separadas por punto
        if (parts[1].length <= 2) {
          // La parte decimal tiene 1-2 dígitos: es formato decimal
          // Ejemplos: 123.45, 1234.83, 12345.9
          // No hacer nada, ya está en formato correcto
        } else if (parts[1].length === 3) {
          // La parte decimal tiene 3 dígitos: puede ser ambiguo
          // 123.456 podría ser 123456 o 123.456
          // Usamos una heurística: si la parte entera es muy larga (>= 4),
          // probablemente es separador de miles
          if (parts[0].length >= 4) {
            // 1234.567 -> 1234567 (separador de miles)
            cleanValue = cleanValue.replace(/\./g, "");
          } else {
            // 123.456 -> podría ser decimal, lo dejamos como está
            // El usuario puede corregir si no es lo que quería
          }
        } else {
          // Más de 3 dígitos después del punto: separador de miles
          cleanValue = cleanValue.replace(/\./g, "");
        }
      } else {
        // Múltiples puntos: formato separador de miles
        cleanValue = cleanValue.replace(/\./g, "");
      }
    }

    const parsed = parseFloat(cleanValue);
    return isNaN(parsed) ? null : parsed;
  };

  // Función para limpiar valor pegado
  const cleanPastedValue = (value) => {
    // Permitir números, puntos, comas y espacios
    return value.replace(/[^\d.,\s]/g, "");
  };

  // Validaciones computadas
  const computedRules = computed(() => {
    const rules = [...props.customRules];

    if (props.required) {
      rules.push((val) => {
        const parsed = parseFromSpanish(val);
        return (parsed !== null && parsed !== undefined) || "Este campo es obligatorio";
      });
    }

    if (props.numeric) {
      rules.push((val) => {
        if (!val) return true; // Si no es requerido y está vacío, es válido
        const parsed = parseFromSpanish(val);
        return !isNaN(parsed) || "Debe ser un número válido";
      });
    }

    if (props.min !== null) {
      rules.push((val) => {
        if (!val) return true;
        const parsed = parseFromSpanish(val);
        return parsed >= props.min || `El valor mínimo es ${props.min}`;
      });
    }

    if (props.max !== null) {
      rules.push((val) => {
        if (!val) return true;
        const parsed = parseFromSpanish(val);
        return parsed <= props.max || `El valor máximo es ${props.max}`;
      });
    }

    return rules;
  });

  // Watchers
  watch(
    () => props.modelValue,
    (newValue) => {
      if (!isFocused.value) {
        displayValue.value = formatToSpanish(newValue);
      }
    },
    { immediate: true }
  );

  // Métodos
  const onInput = (value) => {
    if (isFocused.value) {
      // Durante la edición, permitir formato más libre
      displayValue.value = value;
    } else {
      const parsed = parseFromSpanish(value);
      emit("update:modelValue", parsed);
    }
  };

  const onPaste = async (event) => {
    event.preventDefault();
    const pastedData = event.clipboardData.getData("text");
    const cleanData = cleanPastedValue(pastedData);

    // Actualizar el valor
    displayValue.value = cleanData;
    await nextTick();

    // Parsear y emitir
    const parsed = parseFromSpanish(cleanData);
    emit("update:modelValue", parsed);

    // Formatear después de un breve delay
    setTimeout(() => {
      if (!isFocused.value) {
        displayValue.value = formatToSpanish(parsed);
      }
    }, 100);
  };

  const onFocus = () => {
    isFocused.value = true;
    // Cuando se enfoca, mostrar valor más limpio para edición
    const parsed = parseFromSpanish(displayValue.value);
    if (parsed !== null) {
      displayValue.value = parsed.toString();
    }
  };

  const onBlur = () => {
    isFocused.value = false;
    const parsed = parseFromSpanish(displayValue.value);
    emit("update:modelValue", parsed);
    displayValue.value = formatToSpanish(parsed);
  };

  // Método público para validar
  const validate = () => {
    return inputRef.value?.validate();
  };

  const resetValidation = () => {
    inputRef.value?.resetValidation();
  };

  // Exponer métodos
  defineExpose({
    validate,
    resetValidation,
    focus: () => inputRef.value?.focus(),
    blur: () => inputRef.value?.blur(),
  });
</script>

<style scoped></style>
