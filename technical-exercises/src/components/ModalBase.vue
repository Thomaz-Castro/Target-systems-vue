<template>
    <div v-if="isVisible" class="modal-background">
      <div class="modal-content">
        <button class="close-button" @click="closeModal">Fechar</button>
        <slot></slot>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps, defineEmits } from 'vue';
  
 defineProps(['isVisible']);
  
  const emit = defineEmits(['close']);
  
  function closeModal() {
    emit('close');
  }
  </script>
  
  <style scoped>
  @import "../assets/styles.css";
  </style>
  