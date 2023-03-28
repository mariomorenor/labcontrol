<template>
  <div class="app">
    <div class="toolbar">
      <button @click="sendingAction = true">Accion</button>
    </div>
    <div class="computers-container">
      <computer v-for="computer in computers" :key="computer.id"></computer>
    </div>
    <acciones @closeModal="sendingAction = false" v-if="sendingAction"></acciones>
  </div>
</template>

<script>
import computer from './components/computer.vue';
import acciones from './components/acciones.vue';
import { ipcRenderer } from 'electron';

export default {
  name: 'App',
  components: {
    computer,
    acciones
  },
  data() {
    return {
      sendingAction: false,
      computers: []
    }
  },
  mounted() {
    ipcRenderer.on("computer", (event, data) => {
      console.log(data)
    });

    ipcRenderer.invoke("computers", {}).then((data) => {
      console.log(data)
    })

  }
}
</script>

<style>
body {
  margin: 0;
}

.app {
  margin: 1rem;
}

.toolbar {
  margin-bottom: 1rem;
}

.computers-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
</style>
