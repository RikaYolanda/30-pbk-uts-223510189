<template>
  <div class="todo-list-container">
    <div class="todo-form-container">
      <h2 class="form-title">Form List Kegiatan</h2>
      <form @submit.prevent="addActivity" class="todo-form">
        <div class="form-group">
          <label for="activity" class="form-label">Kegiatan:</label>
          <input type="text" id="activity" v-model="newActivity" class="form-input">
        </div>
        <div class="form-group">
          <label for="date" class="form-label">Tanggal:</label>
          <input type="date" id="date" v-model="newDate" class="form-input">
        </div>
        <div class="form-group">
          <label for="time" class="form-label">Jam:</label>
          <input type="time" id="time" v-model="newTime" class="form-input">
        </div>
        <div class="form-group">
          <label for="location" class="form-label">Lokasi:</label>
          <input type="text" id="location" v-model="newHobby" class="form-input">
        </div>
        <button type="submit" class="form-button">Daftar</button>
      </form>
    </div>

    <div class="activity-list-container">
      <h2 class="activity-list-title">Daftar Kegiatan</h2>
      <table class="activity-table">
        <thead>
          <tr>
            <th>Status</th>
            <th>Kegiatan</th>
            <th>Tanggal</th>
            <th>Jam</th>
            <th>Lokasi</th>
            <th></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(activity, index) in activities" :key="index">
            <td>
              <input type="checkbox" :checked="activity.completed" @change="toggleCompletion(activity)" class="activity-checkbox">
            </td>
            <td :class="{ 'completed': activity.completed }" class="activity-name">{{ activity.name }}</td>
            <td class="activity-date">{{ activity.date }}</td>
            <td>{{ activity.time }}</td>
            <td>{{ activity.hobby }}</td>
            <td><button @click="cancelActivity(index)" class="activity-cancel-button">Batalkan</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      newActivity: '',
      newDate: '',
      newTime: '',
      newHobby: '',
      activities: []
    };
  },
  methods: {
    addActivity() {
      if (this.newActivity && this.newDate && this.newTime && this.newHobby) {
        this.activities.push({
          name: this.newActivity,
          date: this.newDate,
          time: this.newTime,
          hobby: this.newHobby,
          completed: false
        });
        this.newActivity = '';
        this.newDate = '';
        this.newTime = '';
        this.newHobby = '';
      }
    },
    cancelActivity(index) {
      this.activities.splice(index, 1);
    },
    toggleCompletion(activity) {
      activity.completed = !activity.completed;
    }
  }
});
</script>

<style scoped>
.todo-list-container {
  background-image: url('https://th.bing.com/th/id/OIP.sN5JVaYoLuFnN6_mcfz84AHaNK?w=187&h=333&c=7&r=0&o=5&dpr=1.3&pid=1.7');
  background-size: cover;
  background-position: center;
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  height: 100vh; 
}

.todo-list-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.8); 
  border-radius: 10px;
  margin-top: 20px;
}

.todo-form-container {
  max-width: 600px;
  width: 100%;
}

.todo-form {
  background-color: #eda4f6;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.form-group {
  margin-bottom: 20px;
}

.form-label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
  color: #333;
}

.form-input {
  width: calc(100% - 12px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  transition: border-color 0.3s;
}

.form-input:focus {
  border-color: #672060f8;
}

.form-button {
  background-color: #672066;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.3s;
}

.form-button:hover {
  background-color: #d243df;
}

.activity-list-container {
  margin-top: 20px;
  width: 100%;
  max-width: 600px;
}

.activity-table {
  width: 100%;
  border-collapse: collapse;
}

.activity-table th, .activity-table td {
  padding: 10px;
  border: 1px solid #ddd;
  text-align: left;
}

.activity-table th {
  background-color: #f8f9fa;
  font-weight: bold;
}

.activity-checkbox {
  margin-right: 10px;
}

.activity-name {
  font-weight: bold;
  color: #333;
}

.activity-date {
  min-width: 120px;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.activity-cancel-button {
  background-color: #bd35dcdf;
  color: #fff;
  padding: 6px 12px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 14px;
  transition: background-color 0.3s;
}

.activity-cancel-button:hover {
  background-color: #c82333;
}
</style>
