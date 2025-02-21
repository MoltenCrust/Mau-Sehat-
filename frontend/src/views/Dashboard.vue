<template>
  <div class="flex flex-wrap gap-4 justify-center">
    <Card 
      v-for="(painting, index) in paintings" 
      :key="index" 
      class="card-fixed-height"
    >
      <template #header>
        <div class="card-image-container">
          <Image 
            :src="painting.image" 
            :alt="painting.title" 
            preview
            class="card-image"
          />
        </div>
      </template>
      <template #title>{{ painting.title }}</template>
      <template #subtitle><div class="pb-4">{{ painting.artist }}</div></template>
      <template #content>
        <div class="gap-4 flex mb-4 w-full">
          <div
            class="p-2 w-[35%] rounded-lg border-2 border-transparent"
            :class="{
              'bg-red-500': painting.speaker_status === 'Off',
              'bg-blue-500': painting.speaker_status === 'On'
            }"
          >
            <span class="font-semibold">Status:</span> 
            {{ painting.speaker_status }}
          </div>
          <div class="p-2 w-[65%] rounded-lg border-2">
            <span class="font-semibold">Language:</span> 
            {{ painting.language }}
          </div>
        </div>
        <div class="grid grid-cols-2 gap-4 flex mb-4">
          <div class="p-2 rounded-lg border-2">
            <span class="font-semibold">Floor:</span> 
            {{ painting.location.floor }}
          </div>
          <div class="p-2 rounded-lg border-2">
            <span class="font-semibold">Area:</span> 
            {{ painting.location.area }}
          </div>
        </div>
        <Button 
          v-if="painting.description.length > 200" 
          @click="showDialog(index)"
          label="About"
          severity="secondary"
          text
          class="w-full p-0 text-blue-500"
        />
      </template>
    </Card>

    <Dialog 
      v-model:visible="dialogVisible" 
      :header="selectedPainting?.title"
      modal
      class="w-full md:w-6/12"
    >
      <p class="m-0">{{ selectedPainting?.description }}</p>
    </Dialog>
  </div>

  <footer
      style="text-align: right!; color: grey; margin-top: 10px;">
      Developed by Moses Anthony Kwik @ Calvin Institute of Technology - 2025
  </footer>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import type { Ref } from 'vue'

interface Location {
  floor: number;
  area: string;
}

interface Painting {
  title: string;
  artist: string;
  image: string;
  description: string;
  speaker_status: 'On' | 'Off';
  location: Location;
  language: string;
}

// Initialize the refs with proper typing
const paintings: Ref<Painting[]> = ref([])
const dialogVisible = ref(false)
const selectedPainting: Ref<Painting | null> = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('/paintings.json')
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`)
    }
    const data = await response.json()
    paintings.value = data.paintings
  } catch (error) {
    console.error('Error loading paintings data:', error)
  }
})

const showDialog = (index: number): void => {
  selectedPainting.value = paintings.value[index]
  dialogVisible.value = true
}
</script>

<style scoped>
.card-fixed-height {
  width: 23rem;
  height: 30.7rem;
  display: flex;
  flex-direction: column;
}

.card-image-container {
  height: 13rem;
  overflow: hidden;
  border-radius: 10pt 10pt 0pt 0pt;
  background-color: grey;
  position: relative;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-image :deep(img) {
  width: 100% !important;
  height: 100% !important;
  object-fit: cover !important;
  position: absolute !important;
  top: 0 !important;
  left: 0 !important;
}
</style>