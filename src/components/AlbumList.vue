<template>
  <div>
    <h2>Albums</h2>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Title</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="album in albums" :key="album.id">
          <td>{{ album.id }}</td>
          <td>
            <router-link :to="'/albums/' + album.id">{{ album.title }}</router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import { useAlbumsStore } from '../stores/albums';
import { onMounted } from 'vue';

export default {
  setup() {
    const albumsStore = useAlbumsStore();

    onMounted(() => {
      albumsStore.fetchAlbums();
    });

    return {
      albums: albumsStore.albums
    };
  }
}
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #a218a4f4;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #d91fe6;
  color: white;
}

tr:nth-child(even) {
  background-color: #9a0995;
}

a {
  color: #040404cb;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>
