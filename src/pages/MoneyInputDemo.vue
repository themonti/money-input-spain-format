<template>
  <q-page class="q-pa-lg">
    <div class="text-h3 q-mb-lg">MoneyInput - Componente de Input Monetario</div>

    <q-card class="q-mb-lg">
      <q-card-section>
        <div class="text-h5 q-mb-md">Características principales</div>
        <ul>
          <li>Formato de visualización español: 1.234,56 €</li>
          <li>Valor del v-model en formato internacional: 1234.56</li>
          <li>Soporte para copiar/pegar en múltiples formatos</li>
          <li>Validaciones integradas (obligatorio, numérico, min/max)</li>
          <li>Opciones de disable y readonly</li>
        </ul>
      </q-card-section>
    </q-card>

    <div class="row q-gutter-lg">
      <!-- Ejemplos básicos -->
      <div class="col-12 col-md-5">
        <q-card>
          <q-card-section>
            <div class="text-h6 q-mb-md">Ejemplos básicos</div>

            <div class="q-mb-md">
              <money-input v-model="ejemplo1" label="Campo básico" hint="Ejemplo básico sin validaciones" />
              <div class="text-caption q-mt-xs">Valor: {{ ejemplo1 }}</div>
            </div>

            <div class="q-mb-md">
              <money-input v-model="ejemplo2" label="Campo obligatorio" :required="true" hint="Este campo es obligatorio" />
              <div class="text-caption q-mt-xs">Valor: {{ ejemplo2 }}</div>
            </div>

            <div class="q-mb-md">
              <money-input v-model="ejemplo3" label="Con límites" :required="true" :min="10" :max="1000" hint="Entre 10€ y 1000€" />
              <div class="text-caption q-mt-xs">Valor: {{ ejemplo3 }}</div>
            </div>

            <div class="q-mb-md">
              <money-input v-model="ejemplo4" label="Campo deshabilitado" :disable="true" hint="Este campo está deshabilitado" />
            </div>

            <div class="q-mb-md">
              <money-input v-model="ejemplo5" label="Solo lectura" :readonly="true" hint="Este campo es de solo lectura" />
            </div>
          </q-card-section>
        </q-card>
      </div>

      <!-- Casos de prueba -->
      <div class="col-12 col-md-6">
        <q-card>
          <q-card-section>
            <div class="text-h6 q-mb-md">Casos de prueba</div>

            <div class="q-mb-md">
              <money-input v-model="test1" label="Prueba de formatos" hint="Prueba pegar: 1234, 1234.83, 123.455,09" />
              <div class="text-caption q-mt-xs">Valor: {{ test1 }} ({{ typeof test1 }})</div>
            </div>

            <q-separator class="q-my-md" />

            <div class="text-subtitle2 q-mb-md">Valores para copiar y pegar:</div>
            <div class="q-mb-sm">
              <q-chip clickable @click="copyToClipboard('1234')" icon="content_copy" color="primary" text-color="white"> 1234 </q-chip>
              <q-chip clickable @click="copyToClipboard('1234.83')" icon="content_copy" color="primary" text-color="white"> 1234.83 </q-chip>
              <q-chip clickable @click="copyToClipboard('123.455,09')" icon="content_copy" color="primary" text-color="white"> 123.455,09 </q-chip>
            </div>
            <div class="q-mb-md">
              <q-chip clickable @click="copyToClipboard('12.345.678,99')" icon="content_copy" color="secondary" text-color="white"> 12.345.678,99 </q-chip>
              <q-chip clickable @click="copyToClipboard('987654.32')" icon="content_copy" color="secondary" text-color="white"> 987654.32 </q-chip>
            </div>

            <q-separator class="q-my-md" />

            <div class="text-subtitle2 q-mb-md">Botones de prueba:</div>
            <div class="q-gutter-sm">
              <q-btn color="positive" label="Asignar 1234.56" @click="test1 = 1234.56" />
              <q-btn color="orange" label="Asignar null" @click="test1 = null" />
              <q-btn color="negative" label="Limpiar" @click="clearAll" />
            </div>

            <q-separator class="q-my-md" />

            <div class="text-subtitle2 q-mb-md">Validación personalizada:</div>
            <money-input v-model="testValidation" label="Solo múltiplos de 50" :required="true" :custom-rules="[multipleOf50Rule]" hint="Debe ser múltiplo de 50" />
            <div class="text-caption q-mt-xs">Valor: {{ testValidation }}</div>
          </q-card-section>
        </q-card>
      </div>
    </div>

    <!-- Diseños de Quasar -->
    <div class="row q-gutter-lg q-mt-lg">
      <div class="col-12">
        <q-card>
          <q-card-section>
            <div class="text-h5 q-mb-md">Diseños y Atributos de Quasar</div>

            <div class="row q-gutter-md">
              <div class="col-12 col-md-5">
                <div class="text-h6 q-mb-md">Diseños</div>

                <div class="q-mb-md">
                  <money-input v-model="outlinedExample" label="Outlined" :filled="false" :outlined="true" hint="Diseño con contorno" />
                  <div class="text-caption q-mt-xs">Valor: {{ outlinedExample }}</div>
                </div>

                <div class="q-mb-md">
                  <money-input v-model="standoutExample" label="Standout" :filled="false" :standout="true" hint="Diseño destacado" />
                  <div class="text-caption q-mt-xs">Valor: {{ standoutExample }}</div>
                </div>

                <div class="q-mb-md">
                  <money-input v-model="borderlessExample" label="Borderless" :filled="false" :borderless="true" hint="Sin bordes" />
                  <div class="text-caption q-mt-xs">Valor: {{ borderlessExample }}</div>
                </div>
              </div>

              <div class="col-12 col-md-6">
                <div class="text-h6 q-mb-md">Atributos adicionales</div>

                <div class="q-mb-md">
                  <money-input v-model="denseExample" label="Dense + Color" :dense="true" color="secondary" hint="Versión compacta" />
                  <div class="text-caption q-mt-xs">Valor: {{ denseExample }}</div>
                </div>

                <div class="q-mb-md">
                  <money-input v-model="roundedExample" label="Rounded + Outlined" :filled="false" :outlined="true" :rounded="true" color="purple" hint="Bordes redondeados" />
                  <div class="text-caption q-mt-xs">Valor: {{ roundedExample }}</div>
                </div>

                <div class="q-mb-md">
                  <money-input v-model="clearableExample" label="Clearable + Square" :clearable="true" :square="true" color="teal" hint="Con botón limpiar" />
                  <div class="text-caption q-mt-xs">Valor: {{ clearableExample }}</div>
                </div>
              </div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>

    <!-- Información de estado -->
    <q-card class="q-mt-lg">
      <q-card-section>
        <div class="text-h6 q-mb-md">Estado actual de los valores</div>
        <div class="row">
          <div class="col-12">
            <pre class="bg-grey-2 q-pa-md">{{
              JSON.stringify(
                {
                  ejemplo1,
                  ejemplo2,
                  ejemplo3,
                  ejemplo4: ejemplo4,
                  ejemplo5: ejemplo5,
                  test1,
                  testValidation,
                  outlinedExample,
                  standoutExample,
                  borderlessExample,
                  denseExample,
                  roundedExample,
                  clearableExample,
                },
                null,
                2
              )
            }}</pre>
          </div>
        </div>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
  import { ref } from "vue";
  import { useQuasar } from "quasar";
  import MoneyInput from "../components/MoneyInput.vue";

  const $q = useQuasar();

  // Variables reactivas para los ejemplos
  const ejemplo1 = ref(null);
  const ejemplo2 = ref(null);
  const ejemplo3 = ref(50);
  const ejemplo4 = ref(999.99);
  const ejemplo5 = ref(12345.67);
  const test1 = ref(null);
  const testValidation = ref(null);

  // Variables para ejemplos de diseños
  const outlinedExample = ref(null);
  const standoutExample = ref(null);
  const borderlessExample = ref(null);
  const denseExample = ref(null);
  const roundedExample = ref(null);
  const clearableExample = ref(123.45);

  // Regla de validación personalizada
  const multipleOf50Rule = (val) => {
    if (!val) return true;
    const num = parseFloat(
      val
        .toString()
        .replace(/[^\d.,]/g, "")
        .replace(",", ".")
    );
    return num % 50 === 0 || "Debe ser múltiplo de 50";
  };

  // Método para copiar al portapapeles
  const copyToClipboard = async (text) => {
    try {
      await navigator.clipboard.writeText(text);
      $q.notify({
        message: `Copiado: ${text}`,
        color: "positive",
        position: "top",
        timeout: 1000,
      });
    } catch {
      $q.notify({
        message: "Error al copiar",
        color: "negative",
        position: "top",
      });
    }
  };

  // Método para limpiar todos los valores
  const clearAll = () => {
    ejemplo1.value = null;
    ejemplo2.value = null;
    ejemplo3.value = null;
    test1.value = null;
    testValidation.value = null;
    outlinedExample.value = null;
    standoutExample.value = null;
    borderlessExample.value = null;
    denseExample.value = null;
    roundedExample.value = null;
    clearableExample.value = null;
  };
</script>

<style scoped>
  pre {
    font-family: "Courier New", monospace;
    border-radius: 4px;
    overflow-x: auto;
  }
</style>
