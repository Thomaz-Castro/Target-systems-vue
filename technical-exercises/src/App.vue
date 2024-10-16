<template>
  <div class="app-container">
    <h1>Escolha uma opção</h1>
    <div class="grid-container">
      <div v-for="(item, index) in gridItems" :key="index" class="grid-item" @click="onItemClick(item)">
        <h3>{{ item.label }}</h3>
      </div>
    </div>
    <div class="components-container">
      <SomaK :isOpen="selectedComponent === 'SomaK'" @close="selectedComponent = null" />
      <FibonacciSeries :isOpen="selectedComponent === 'FibonacciSeries'" @close="selectedComponent = null" />
      <FaturamentoDiario :isOpen="selectedComponent === 'FaturamentoDiario'" @close="selectedComponent = null" />
      <FaturamentoPorEstado :isOpen="selectedComponent === 'FaturamentoPorEstado'" @close="selectedComponent = null" />
      <InverterString :isOpen="selectedComponent === 'InverterString'" @close="selectedComponent = null" />
    </div>
    <footer>
      <a :href="linkedinUrl" target="_blank" class="linkedin-link">Conecte-se comigo no LinkedIn</a>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Importação dos componentes
import SomaK from './components/SomaK.vue';
import FibonacciSeries from './components/FibonacciSeries.vue';
import FaturamentoDiario from './components/FaturamentoDiario.vue';
import FaturamentoPorEstado from './components/FaturamentoPorEstado.vue';
import InverterString from './components/InverterString.vue';

// Lista de itens do grid
const gridItems = ref([
  { label: 'Soma K', component: 'SomaK' },
  { label: 'Fibonacci Series', component: 'FibonacciSeries' },
  { label: 'Faturamento Diário', component: 'FaturamentoDiario' },
  { label: 'Faturamento por Estado', component: 'FaturamentoPorEstado' },
  { label: 'Inverter String', component: 'InverterString' },
]);

// URL do LinkedIn
const linkedinUrl = ref('https://www.linkedin.com/in/thomaz-castro-243605233/');

// Estado para componente selecionado
const selectedComponent = ref(null);

// Função ao clicar em um item
const onItemClick = (item) => {
  selectedComponent.value = item.component;
};
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  background-color: #f4f4f4;
  font-family: 'Arial', sans-serif;
}

h1 {
  margin-bottom: 20px;
  color: #333;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 20px;
  width: 80%;
  max-width: 1000px;
}

.grid-item {
  background-color: #ffffff;
  border: 2px solid #007bff;
  border-radius: 10px;
  padding: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.grid-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

.grid-item h3 {
  color: #007bff;
  font-size: 16px;
  font-weight: bold;
}

.components-container {
  margin-top: 40px;
  width: 80%;
  display: flex;
  justify-content: center;
}

footer {
  margin-top: 30px;
}

.linkedin-link {
  color: #007bff;
  text-decoration: none;
  font-size: 16px;
}
</style>
