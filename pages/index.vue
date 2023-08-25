<template>
  <div  class="grid-container">
    <div v-if="loading">Loading...</div>
    <div v-for="photo in photos" :key="photo.id" class="grid-item" v-else>
      <img class="grid-image" :src="photo.urls.regular" :alt="photo.alt_description" />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: true, 
      photos: [],
    };
  },
  async created() {
    const Authorization = 'jsObqdRThoNK5Yi1n3yHG3X8s_maInFgnkjwJm7FV_8';
    try {
      const response = await fetch(`https://api.unsplash.com/photos/?client_id=${Authorization}`);
      const data = await response.json();
      this.photos = data;
      this.loading = false; 
    } catch (error) {
      console.error('Fotoğraflar güklenirken hata oluştu:', error);
      this.loading = false; 
    }
  },
};
</script>

<style scoped>
.grid-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
}

.grid-item {
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
}

.grid-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 5px;
}
</style>
