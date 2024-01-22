<script setup>
import axios from 'axios';
import { ref } from 'vue';
import Dashboard from '@/components/Dashboard.vue';
import Swal from 'sweetalert2';

const fileInput = ref(null);
const fileSelected = ref(false)
const chartDataMRR = ref(null);
const chartDataCR = ref(null);

const uploadFile = async () => {
  [chartDataMRR.value, chartDataCR.value] = [null, null];
  fileSelected.value = false;

  const file = await fileInput.value.files[0];
  const formData = new FormData();
  formData.append('file', file);

  try {
    const response = await axios.post('http://localhost:3000/upload', formData, {
      headers: { 'Content-Type': 'multipart/form-data' }
    });
    if(response) [chartDataMRR.value, chartDataCR.value] = [response.data.result.mrr, response.data.result.cr];
  } catch (error) {
    Swal.fire({ icon: 'error', title: 'Erro', text: 'Os dados do seu arquivo não são compatíveis.' });
    console.log(error)
  }

  fileInput.value.value = '';
}

const handleFileChange = (event) => {
  fileSelected.value = event.target.files.length > 0;
} 
</script>

<template>
  <main>
    <h1>Bem Vindo(a) ao <span>MetricHub</span></h1> 
    <p>Faça o upload das suas planilhas para extrair métricas importantes.</p>
    <form @submit.prevent="uploadFile">
      <input type="file" accept=".xlsx, .csv" ref="fileInput" @change="handleFileChange">
      <button type="submit" :disabled="!fileSelected">Gerar Dashboard</button>
    </form>
    <Dashboard v-if="chartDataMRR && chartDataCR" :chartDataMRR="chartDataMRR" :chartDataCR="chartDataCR" /> 
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 50px;
}

h1 {
  color: #41167F;
  margin-top: 50px;
  text-align: center;
}

p {
  text-align: center;
}

h1 span {
  color: #fff;
  background-color: #41167F;
  padding: 3px;
  border-radius: 7px;
}

form {
  max-width: 400px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: #41167F;
  color: #fff;
  gap: 20px;
  padding: 30px;
  border-radius: 7px;
}

button, input {
  background-color: #0D9D68;
  padding: 7px;
  border-radius: 7px;
  color: #fff;
  border: none;
  cursor: pointer;
}

input {
  background-color: #fff;
  color: #41167F;
}

button:active:hover {
  opacity: 0.75;
}

button:disabled {
  background-color: #AFB1B3;
}

@media screen and (max-width: 350px) {
  form {
    width: 90vw;
    padding: 20px 10px;
    gap: 25px;
  }

  button, input {
    width: 100%;
  }

  button {
    font-size: 0.8rem;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; 
  }

  h1 {
    font-size: 1.3em;
  }
  p {
    font-size: 0.9em;
  }
  
} 


</style>
