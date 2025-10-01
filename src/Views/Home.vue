<template>
  <div>
    <Draggable v-model="cards" class="grid-container" item-key="id" :disabled="!editMode">
      <template #item="{ element }">
        <div class="card">
          <h2 class="card-title">{{ element.title }}</h2>

          <DataTable
            v-if="element.content === 'datatable'"
            :value="gpsData"
            paginator
            :rows="5"
            class="responsive-table"
          >
            <Column field="Marca de tiempo" header="Tiempo" sortable />
            <Column field="id_gps" header="ID GPS" sortable />
            <Column field="latitud" header="Latitud" sortable />
            <Column field="longitud" header="Longitud" sortable />
            <Column field="Speed(km/h)" header="Velocidad" sortable />
            <Column field="Direction" header="Dirección" sortable />
          </DataTable>

          <div v-else class="empty-content">No hay datos disponibles</div>
        </div>
      </template>
    </Draggable>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Draggable from 'vuedraggable'
import DataTable from 'primevue/datatable'
import Column from 'primevue/column'
import { emitter } from '/src/utils/eventBus.js' // Importamos el event bus

const gpsData = ref([])
const editMode = ref(false) // Controla si se puede mover

const cards = ref([
  { id: 1, title: 'Datos GPS 1', content: 'datatable' },
  { id: 2, title: 'Datos GPS 2', content: 'empty' },
  { id: 3, title: 'Datos GPS 3', content: 'empty' },
  { id: 4, title: 'Datos GPS 4', content: 'empty' },
])

onMounted(async () => {
  try {
    const res = await fetch('http://127.0.0.1:5000/gps')
    gpsData.value = await res.json()
  } catch (err) {
    console.error('Error al cargar datos GPS:', err)
  }

  emitter.on('toggleEdit', (value) => {
    editMode.value = value
  })
})
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-auto-rows: 1fr;
  gap: 2rem;
  margin: 2rem;
  align-items: stretch;
}

.card {
  display: flex;
  flex-direction: column;
  padding: 1rem;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.card-title {
  text-align: center;
  font-size: 1.3rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.responsive-table {
  width: 100%;
  flex-grow: 1;
}

.empty-content {
  flex-grow: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #888;
  font-style: italic;
}
</style>
