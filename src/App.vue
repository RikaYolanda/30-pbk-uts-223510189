<template>
  <div>
    <header class="header">
      <nav class="menu">
        <ul>
          <li><h2><router-link to="/todos">Todos</router-link></h2></li>
          <li><h2><router-link to="/posts">Posts</router-link></h2></li>
          <li><h2><router-link to="/albums">Albums</router-link></h2></li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>


<style scoped>

.header {
  background-color: #483b64;
  padding: 0px;
  text-align: center;
}

.menu ul {
  display: flex;
  justify-content: center;
  list-style: none;
  padding: 0;
  margin: 0;
}

.menu ul li {
  margin: 0 10px;
}

.menu ul li a {
  text-decoration: none;
  color: #f0f0f0; 
  font-weight: bold;
  font-size: 30px; 
  padding: 5px 10px; 
  border-radius: 20px; 
  transition: background-color 0.3s, transform 0.3s; 
}

.menu ul li a:hover {
  background-color: #255b7c; 
  transform: scale(1.05); 
}
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px;
  background-color: #faf3e0;
  min-height: 100vh; 
}

.button-container {
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  margin: 0 10px;
  background-color: #675720;
  color: white;
  border: none;
  cursor: pointer;
  border-radius: 5px;
  font-size: 16px;
  transition: background-color 0.3s, transform 0.3s;
}

button:hover {
  background-color: #675720;
  transform: scale(1.05);
}

button.active {
  background-color: #a08645;
  color: #fff;
  font-weight: bold;
}

.content-container {
  width: 100%;
  max-width: 800px; 
  background-color: #ffffff;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); 
  transition: all 0.3s ease;
}

.content-container > *:not(:last-child) {
  margin-bottom: 20px; 
}
</style>
