<template>
    <div>
      <modal-base :isVisible="isOpen" @close="$emit('close')">
        <h2>Soma de K</h2>
        <p>Resultado da soma: {{ soma }}</p>
        <button @click="calcularSoma">Calcular Soma</button>
      </modal-base>
    </div>
  </template>
  
  <script setup>
  import { ref, defineProps, defineEmits } from 'vue';
  import ModalBase from './ModalBase.vue';
  
  defineEmits(['close']);
  defineProps(['isOpen']);
  const soma = ref(0);
  
  function calcularSoma() {
    let INDICE = 13;
    let SOMA = 0;
    let K = 0;
  
    while (K < INDICE) {
      K = K + 1;
      SOMA = SOMA + K;
    }
    
    soma.value = SOMA;
  }
  </script>
  