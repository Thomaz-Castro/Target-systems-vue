<template>
    <div>
      <modal-base :isVisible="isOpen" @close="$emit('close')">
        <h2>Sequência de Fibonacci</h2>
        <input v-model.number="numero" placeholder="Digite um número" />
        <button @click="verificarFibonacci">Verificar</button>
        <p>{{ mensagem }}</p>
      </modal-base>
    </div>
  </template>
  
  <script setup>
  import { ref, defineProps, defineEmits } from 'vue';
  import ModalBase from './ModalBase.vue';
  
  defineEmits(['close']);
  defineProps(['isOpen']);

  const numero = ref(0);
  const mensagem = ref('');
  
  function verificarFibonacci() {
    let a = 0, b = 1;
    let pertence = false;
  
    while (a <= numero.value) {
      if (a === numero.value) {
        pertence = true;
        break;
      }
      [a, b] = [b, a + b];
    }
  
    mensagem.value = pertence ? 'O número pertence à sequência de Fibonacci.' : 'O número não pertence à sequência de Fibonacci.';
  }
  </script>
  