<template>
    <div>
    
      <modal-base :isVisible="isOpen" @close="$emit('close')">
        <h2>Faturamento Diário</h2>
        <input type="file" @change="importarJson" />
        <button @click="baixarExemplo">Baixar Exemplo</button>
        <div v-if="faturamento.length > 0">
          <p>Menor faturamento: {{ menor }}</p>
          <p>Maior faturamento: {{ maior }}</p>
          <p>Dias com faturamento acima da média: {{ acimaMedia }}</p>
        </div>
      </modal-base>
    </div>
  </template>
  
  <script setup>
  import { defineProps, ref, computed, defineEmits } from 'vue';
  import ModalBase from './ModalBase.vue';
  
  defineEmits(['close']);
  defineProps(['isOpen']);
  const faturamento = ref([]);
  const menor = computed(() => Math.min(...faturamento.value.map(dia => dia.valor)));
  const maior = computed(() => Math.max(...faturamento.value.map(dia => dia.valor)));
  const media = computed(() => {
    const diasValidos = faturamento.value.filter(dia => dia.valor > 0);
    return diasValidos.reduce((acc, dia) => acc + dia.valor, 0) / diasValidos.length;
  });
  const acimaMedia = computed(() => faturamento.value.filter(dia => dia.valor > media.value).length);
  
  function importarJson(event) {
    const file = event.target.files[0];
    const reader = new FileReader();
    reader.onload = function(e) {
      try {
        const json = JSON.parse(e.target.result);
        if (Array.isArray(json)) {
          faturamento.value = json;
        } else {
          alert('JSON inválido.');
        }
      } catch (error) {
        alert('Erro ao processar o arquivo JSON.');
      }
    };
    reader.readAsText(file);
  }
  
  function baixarExemplo() {
    const exemplo = [
      { dia: "01/10/2024", valor: 1000 },
      { dia: "02/10/2024", valor: 2000 },
      { dia: "03/10/2024", valor: 0 }, // Sem faturamento
      { dia: "04/10/2024", valor: 3000 }
    ];
    const blob = new Blob([JSON.stringify(exemplo)], { type: 'application/json' });
    const link = document.createElement('a');
    link.href = URL.createObjectURL(blob);
    link.download = 'faturamento-exemplo.json';
    link.click();
  }
  </script>
  