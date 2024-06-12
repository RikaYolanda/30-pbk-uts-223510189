<template>
  <div class="post-container">
    <h2 class="post-title">Post</h2>
    <select v-model="selectedUser" @change="fetchPosts" class="post-select">
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>
    <div v-for="post in posts" :key="post.id" class="post-item">
      <h3 class="post-item-title">{{ post.title }}</h3>
      <p class="post-item-body">{{ post.body }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue';

export default defineComponent({
  setup() {
    const users = ref([]);
    const selectedUser = ref(null);
    const posts = ref([]);

    const fetchUsers = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/users');
        if (!response.ok) {
          throw new Error('Failed to fetch users');
        }
        users.value = await response.json();
      } catch (error) {
        console.error(error);
      }
    };

    const fetchPosts = async () => {
      if (!selectedUser.value) return;

      try {
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
        if (!response.ok) {
          throw new Error('Failed to fetch posts');
        }
        posts.value = await response.json();
      } catch (error) {
        console.error(error);
      }
    };

    onMounted(fetchUsers);

    return { users, selectedUser, posts, fetchPosts };
  }
});
</script>

<style scoped>
.post-container {
  background-image: url('https://th.bing.com/th/id/OIP.CHOtVpmI9xxMgr6YVa-GfAHaMY?w=193&h=323&c=7&r=0&o=5&dpr=1.3&pid=1.7');
  background-size: cover;
  background-position: center;
  margin: 0;
  padding: 0;
}
body {
  background-image: url('https://th.bing.com/th/id/OIP.CHOtVpmI9xxMgr6YVa-GfAHaMY?w=193&h=323&c=7&r=0&o=5&dpr=1.3&pid=1.7');
  background-size: cover;
  background-position: center;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
}

.post-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  background-color: #e0d4f3;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.post-title {
  text-align: center;
  margin-bottom: 20px;
  font-size: 24px;
  color: #5d3c8c;
}

.post-select {
  display: block;
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  background-color: #e0d4f3;
  color: #5d3c8c;
}

.post-item {
  margin-bottom: 20px;
  background-color: #f2eafc;
  padding: 15px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.post-item-title {
  font-size: 20px;
  margin-bottom: 10px;
  color: #4b2c72;
}

.post-item-body {
  font-size: 16px;
  color: #4b2c72;
}
</style>
