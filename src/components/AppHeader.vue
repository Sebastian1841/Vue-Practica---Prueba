<template>
  <div>
    <Menubar :model="itemsSmall" class="menubar-small">
      <template #item="{ item, props }">
        <a 
          v-ripple 
          class="flex items-center small-item" 
          v-bind="props.action" 
          @click="handleClick(item)"
        >
          <span>{{ item.label }}</span>
        </a>
      </template>
    </Menubar>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Menubar from 'primevue/menubar'
import { emitter } from '/src/Utils/eventBus.js'

const editMode = ref(false) // controla si estamos editando

const itemsSmall = ref([
  { label: 'Editar' } // inicial
])

const handleClick = (item) => {
  if (item.label === 'Editar') {
    editMode.value = true
    itemsSmall.value = [{ label: 'Cancelar' }] // cambia a Cancelar
    emitter.emit('toggleEdit', true)
  } else if (item.label === 'Cancelar') {
    editMode.value = false
    itemsSmall.value = [{ label: 'Editar' }] // vuelve a Editar
    emitter.emit('toggleEdit', false)
  }
}
</script>

<style scoped>
.menubar-small {
  font-size: 0.8rem;
  padding: 0.25rem 0.5rem;
}

.menubar-small .small-item {
  padding: 0.25rem 0.5rem;
}
</style>
