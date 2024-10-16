<template>
    <div>
      <modal-base :isVisible="isOpen" @close="$emit('close')">
        <h2>Inversão de String</h2>
        <input v-model="inputString" placeholder="Digite uma string" />
        <button @click="inverterString">Inverter</button>
        <p>String invertida: {{ stringInvertida }}</p>
      </modal-base>
    </div>
  </template>
  
  <script setup>
  import { ref, defineProps, defineEmits} from 'vue';
  import ModalBase from './ModalBase.vue';
  
  defineEmits(['close']);
  defineProps(['isOpen']);
  const inputString = ref('');
  const stringInvertida = ref('');
  
  function inverterString() {
    const str = inputString.value; // Acesso à string original
    let chars = str.split(''); // Converte a string em um array de caracteres
    let a, b; // Variáveis auxiliares
    
    // Itera sobre a primeira metade da string
    for (let i = 0; i < Math.floor(chars.length / 2); i++) {
        a = chars[i]; // Armazena o caractere da posição i
        b = chars[chars.length - 1 - i]; // Armazena o caractere da posição correspondente no final

        // Troca os caracteres
        chars[i] = b;
        chars[chars.length - 1 - i] = a;
    }

    // Converte o array de volta para uma string
    stringInvertida.value = chars.join(''); // Atribui o resultado a stringInvertida
}

  </script>
  