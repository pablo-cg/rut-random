<script setup>
import { validate, format } from "@fiquu/cl-rut";
import { ref } from "vue";

const ruts = ref([]);
const enClipboard = ref("");
const copiados = ref([]);

const getRutNoValidado = () => {
  const guiones = "0123456789K";
  const digitos = getRandomNumber(3000000, 25000000);
  const dVerificador = guiones.charAt(getRandomNumber(0, 10));
  const rutNoValidado = `${digitos}-${dVerificador}`;
  return rutNoValidado;
};

const getRandomNumber = (min, max) => {
  return Math.floor(Math.random() * (max - min + 1)) + min;
};

const getRut = () => {
  let rut = "";
  while (!validate(rut)) {
    rut = getRutNoValidado();
  }
  return format(rut);
};

const generarRutsAleatorio = () => {
  ruts.value = [];
  for (let i = 0; i < 10; i++) {
    ruts.value.push(getRut());
  }
};

const copiar = (texto) => {
  navigator.clipboard.writeText(texto);
  enClipboard.value = texto;
  copiados.value.push(texto);
};

const disabled = (texto) => {
  const encuentra = copiados.value.find((rut) => rut == texto);
  if (encuentra) {
    return true;
  } else {
    return false;
  }
};
</script>

<template>
  <div class="container mx-auto">
    <section class="text-center my-5">
      <button
        class="bg-green-600 text-2xl hover:bg-green-900 text-white py-2 px-7 rounded-full"
        @click="generarRutsAleatorio"
      >
        Generar
      </button>
    </section>
    <div v-if="ruts.length > 0" class="flex justify-around">
      <table class="table-auto text-lg">
        <tbody>
          <tr v-for="rut in ruts" :key="rut">
            <td class="px-3 py-2" :class="disabled(rut) ? 'line-through' : ''">
              {{ rut }}
            </td>
            <td class="px-3">
              <button
                class="bg-green-600 hover:bg-green-900 text-white py-1 px-5 rounded-full disabled:bg-green-200 disabled:text-black"
                @click="copiar(rut)"
                :disabled="disabled(rut)"
              >
                {{ disabled(rut) ? "Copiado" : "Copiar" }}
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
