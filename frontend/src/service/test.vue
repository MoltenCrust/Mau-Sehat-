<template>
    <div class="flex flex-wrap gap-4">
      <Card 
        v-for="(painting, index) in paintings" 
        :key="index" 
        class="card-fixed-height"
      >
        <template #header>
          <div class="card-image-container">
            <img 
              :src="painting.image" 
              :alt="painting.title" 
              class="card-image"
            />
          </div>
        </template>
        <template #title>{{ painting.title }}</template>
        <template #subtitle>{{ painting.artist }}</template>
        <template #content>
          <p class="card-description" :class="{ 'expanded': painting.isExpanded }">
            {{ painting.description }}
          </p>
          <button 
            v-if="painting.description.length > 200" 
            @click="toggleDescription(index)"
            class="see-more-btn"
          >
            {{ painting.isExpanded ? 'See Less' : 'See More' }}
          </button>
        </template>
        <template #footer>
          <div class="flex gap-4 mt-1">
            <Button label="Cancel" severity="secondary" outlined class="w-full" />
            <Button label="Save" class="w-full" />
          </div>
        </template>
      </Card>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const paintings = ref([
    {
      title: 'The Last Supper',
      artist: 'Leonardo da Vinci (1495–1498)',
      image: '/paintings/The Last Supper - Leonardo Da Vinci.avif',
      description: 'A masterclass in composition and perspective, drawing the viewer\'s eye toward Jesus at the center, framed by the receding lines of the room. The apostles\' dynamic gestures and facial expressions capture a range of emotions, reinforcing the drama of Jesus\' revelation. The use of light and shadow enhances depth, while Leonardo\'s innovative fresco technique, though prone to deterioration, adds a soft, atmospheric quality that heightens the painting\'s realism.',
      isExpanded: false
    },
    {
      title: 'The Creation of Adam',
      artist: 'Michelangelo (1511–1512)',
      image: '/paintings/The Creation of Adam - Michelangelo.jpg',
      description: 'This fresco exemplifies Michelangelo\'s expertise in anatomy and movement, with the muscular figures of God and Adam mirroring each other, emphasizing their divine connection. The nearly touching hands symbolize the moment of life\'s transmission, capturing both power and vulnerability. The energetic figures surrounding God, possibly representing angels or personifications of divine intellect, add to the complexity, while the vast emptiness between the hands heightens the painting\'s tension and significance.',
      isExpanded: false
    }
  ])
  
  const toggleDescription = (index) => {
    paintings.value[index].isExpanded = !paintings.value[index].isExpanded
  }
  </script>
  
  <style scoped>
  .card-fixed-height {
    width: 25rem;
    height: 32rem; /* Fixed height for cards */
    display: flex;
    flex-direction: column;
  }
  
  .card-image-container {
    height: 15rem; /* Fixed height for image container */
    overflow: hidden;
  }
  
  .card-image {
    width: 100%;
    height: 100%;
    object-fit: cover; /* Ensures image fills the container while maintaining aspect ratio */
  }
  
  .card-description {
    max-height: 6rem; /* Limit description height */
    overflow: hidden;
    text-overflow: ellipsis;
    transition: max-height 0.3s ease;
  }
  
  .card-description.expanded {
    max-height: none; /* Expand when clicked */
  }
  
  .see-more-btn {
    color: blue;
    background: none;
    border: none;
    cursor: pointer;
    margin-top: 0.5rem;
  }
  </style>