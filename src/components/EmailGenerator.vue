<script setup>
import { ref } from "vue";

const emails = ref([]);
const enClipboard = ref("");
const copiados = ref([]);

const cadenaAleatoria = (longitud, isDomain) => {
  const banco = isDomain
    ? "abcdefghijklmnopqrstuvwxyz"
    : "abcdefghijklmnopqrstuvwxyz0123456789";

  let aleatoria = "";
  for (let i = 0; i < longitud; i++) {
    aleatoria += banco.charAt(Math.floor(Math.random() * banco.length));
  }
  return aleatoria;
};

const getEmail = () => {
  const user = cadenaAleatoria(5);
  const domainName = cadenaAleatoria(5);
  const domain = cadenaAleatoria(2, true);
  return `${user}@${domainName}.${domain}`;
};

const generarEmailsAleatorios = () => {
  emails.value = [];
  for (let i = 0; i < 10; i++) {
    emails.value.push(getEmail());
  }
};

const copiar = (texto) => {
  navigator.clipboard.writeText(texto);
  enClipboard.value = texto;
  copiados.value.push(texto);
};

const disabled = (texto) => {
  return copiados.value.find((rut) => rut == texto);
};
</script>

<template>
  <div class="container mx-auto">
    <section class="text-center my-5">
      <button
        class="bg-green-600 text-2xl hover:bg-green-900 text-white py-2 px-7 rounded-full"
        @click="generarEmailsAleatorios"
      >
        Generar
      </button>
    </section>
    <div v-if="emails.length > 0" class="flex justify-around">
      <table class="table-auto text-lg">
        <tbody>
          <tr v-for="email in emails" :key="email">
            <td
              class="px-3 py-2"
              :class="disabled(email) ? 'line-through' : ''"
            >
              {{ email }}
            </td>
            <td class="px-3">
              <button
                class="bg-green-600 hover:bg-green-900 text-white py-1 px-5 rounded-full disabled:bg-green-200 disabled:text-black"
                @click="copiar(email)"
                :disabled="disabled(email)"
              >
                {{ disabled(email) ? "Copiado" : "Copiar" }}
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
