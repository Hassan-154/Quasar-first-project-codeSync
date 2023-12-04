<template>
  <div>
    <q-table
      :rows="todos"
      :columns="columns"
      row-key="id"
      :loading="loading"
      virtual-scroll-item-size="100"
    >
      <q-tr v-for="row in todos" :key="row.id">
        <q-td auto-width v-for="col in columns" :key="col.name">
          {{ row[col.field] }}
        </q-td>
      </q-tr>
    </q-table>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const todos = ref([]);
const loading = ref(true);

const columns = [
  { name: 'id', align: 'left', label: 'ID', field: 'id', sortable: true },
  { name: 'title', align: 'left', label: 'Title', field: 'title', sortable: true },
  { name: 'complete', align: 'left', label: 'Complete', field: 'complete', sortable: true }
];

function fetchData() {
  axios.get('https://jsonplaceholder.typicode.com/todos')
    .then((response) => {
      todos.value = response.data;
      loading.value = false;
      console.log(response)
    })
    .catch((error) => {
      console.error('Error fetching data:', error);
      loading.value = false;
    });
}

onMounted(() => {
  fetchData();
});
</script>

<style>
/* Your styles here */
</style>
