<template>
  <div id="app">
    <!-- Navbar -->
    <Menubar :model="items">
      <template #item="{ item, props, hasSubmenu, root }">
        <a v-ripple class="flex items-center" v-bind="props.action" @click="handleClick(item)">
          <span>{{ item.label }}</span>
          <Badge v-if="item.badge" :class="{ 'ml-auto': !root, 'ml-2': root }" :value="item.badge" />
          <span v-if="item.shortcut" class="ml-auto border border-surface rounded bg-emphasis text-muted-color text-xs p-1">
            {{ item.shortcut }}
          </span>
          <i v-if="hasSubmenu" :class="['pi pi-angle-down ml-auto', { 'pi-angle-down': root, 'pi-angle-right': !root }]"></i>
        </a>
      </template>


    </Menubar>

    <router-view />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import Menubar from 'primevue/menubar'
import Badge from 'primevue/badge'


const router = useRouter()

const items = ref([
  { label: 'Home', icon: 'pi pi-home', route: { name: 'Home' } },
  { label: 'About', icon: 'pi pi-info-circle', route: { name: 'About' } },
])

const handleClick = (item) => {
  if (item.route) {
    router.push(item.route)
  }
}
</script>
