<template>
    <div>
      <modal-base :isVisible="isOpen" @close="$emit('close')">
        <h2>Faturamento por Estado</h2>
        <ul>
          <li v-for="(percentual, estado) in percentuais" :key="estado">{{ estado }}: {{ percentual.toFixed(2) }}%</li>
        </ul>
      </modal-base>
    </div>
  </template>
  
  <script setup>
  import { defineProps, computed, defineEmits } from 'vue';
  import ModalBase from './ModalBase.vue';
  
  defineEmits(['close']);
  defineProps(['isOpen']);
  const faturamento = {
    SP: 67836.43,
    RJ: 36678.66,
    MG: 29229.88,
    ES: 27165.48,
    Outros: 19849.53,
  };
  const total = computed(() => Object.values(faturamento).reduce((acc, val) => acc + val, 0));
  const percentuais = computed(() => {
    let result = {};
    for (let estado in faturamento) {
      result[estado] = (faturamento[estado] / total.value) * 100;
    }
    return result;
  });
  </script>
  