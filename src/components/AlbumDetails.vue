<template>

    <div class="AlbumDetails-container">
      <table v-if="photos.length" class="photo-table">
        <thead>
          <tr>
            <th>No</th>
            <th>Thumbnail</th>
            <th>Title</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(photo, index) in photos" :key="photo.id">
            <td>{{ index + 1 }}</td>
            <td>
              <img :src="photo.thumbnailUrl" @click="showPhoto(photo.url)" class="thumbnail">
            </td>
            <td>{{ photo.title }}</td>
          </tr>
        </tbody>
      </table>
      <div v-else class="no-photos">
        <p>No photos available.</p>
      </div>
    </div>

</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const selectedAlbum = ref(route.params.id)
const photos = ref([])

const fetchPhotos = async () => {
  try {
    const response = await fetch(`https://jsonplaceholder.typicode.com/albums/${selectedAlbum.value}/photos`)
    photos.value = await response.json()
  } catch (error) {
    console.error('Error fetching photos:', error)
  }
}

const showPhoto = (url) => {
  window.open(url, '_blank')
}

onMounted(() => {
  fetchPhotos()
})
</script>

<style scoped>
body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.menu-bar {
  width: 100%;
  background-color: #000;
  color: #fff;
  padding: 10px 0;
  text-align: center;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1000;
}

.menu-bar a {
  color: #fff;
  text-decoration: none;
  margin: 0 15px;
}

.AlbumDetails-container {
  display: flex;
  justify-content: center;
  align-items: flex-start; 
  flex-direction: column;
  padding-top: 60px; 
  min-height: 100vh;
  background-size: cover;
  background-position: center;
  overflow-x: auto; 
}

.photo-table {
  width: 100%;
  max-width: 800px;
  border-collapse: collapse;
  margin: 20px; 
}

.photo-table th, .photo-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

.thumbnail {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border: 1px solid #007bff;
  border-radius: 5px;
  cursor: pointer;
  transition: border-color 0.3s;
}

.thumbnail:hover {
  border-color: #0056b3;
}

.no-photos {
  text-align: center;
  margin-top: 20px;
}
</style>
