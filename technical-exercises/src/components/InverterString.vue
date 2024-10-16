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
    stringInvertida.value = inputString.value.split('').reverse().join('');
  }
  </script>
  