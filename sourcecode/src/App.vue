<script setup lang="ts">
import { ref } from 'vue';
import RowRol from './components/RowRol.vue';
import IRowRol from './models/IRowRol';
import Divider from 'primevue/divider';
import Tag from 'primevue/tag';

  const showInput = ref(true);
  const file = ref<File | null>();
  const form = ref<HTMLFormElement>();
  const Roles = ref<IRowRol[]>();

  const onFileChanged = async($event: Event) => {
      const target = $event.target as HTMLInputElement;
      if (target && target.files) {
          file.value = target.files[0];
          if(file.value.name.includes(".json")){
            const data = await file.value.text();
            Roles.value = JSON.parse(data);    
            showInput.value = false;    
          }else{
            alert("Solo .Json")
          }
      }
  }
</script>

<template>
  <div class="App">
      <div v-if="showInput">
        <label for="uploadFile">Seleciona el .json a mostrar</label><br>
        <input type="file" name="" id="uploadFile" @change="onFileChanged($event)" accept=".json" >
      </div>
      <div class="connet" v-else>
        <h4 class="m-0">Aldeanos</h4>
        <!-- townsfolk -->
        <RowRol v-for="(item, index) in Roles?.filter(x=>x.team == 'townsfolk')" :key="index" :Rol="item"></RowRol>        
        <h4 class="m-0">Foraneos</h4>
        <!-- outsider -->
        <RowRol v-for="(item, index) in Roles?.filter(x=>x.team == 'outsider')" :key="index" :Rol="item"></RowRol>
        <h4 class="m-0">Minions</h4>
        <!-- minion -->
        <RowRol v-for="(item, index) in Roles?.filter(x=>x.team == 'minion')" :key="index" :Rol="item"></RowRol>
        <h4 class="m-0">Demonios</h4>
        <!-- demon -->
        <RowRol v-for="(item, index) in Roles?.filter(x=>x.team == 'demon')" :key="index" :Rol="item"></RowRol>
      </div>
  </div>
</template>

<style scoped>
  .conten {
    width: 21.6cm;
    height: 27.9cm;
}
p{
  font-size: 12pt !important;
}
</style>
