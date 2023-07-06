<template>
  <div>
    <nav>
      <div class="top-buttons">
        <router-link to="/">
          <button :class="{ active: $route.path === '/home' }">Home</button>
        </router-link>
        <router-link to="/weather">
          <button :class="{ active: $route.path === '/weather' }">Cuaca</button>
        </router-link>
        <router-link to="/location">
          <button :class="{ active: $route.path === '/location' }">Lokasi</button>
        </router-link>
        <router-link to="/stopwatch">
          <button :class="{ active: $route.path === '/stopwatch' }">Stopwatch</button>
        </router-link>
        <router-link to="/tictactoe">
          <button :class="{ active: $route.path === '/rockpaperscissors' }">Game</button>
        </router-link>
        <router-link to="/photo">
          <button :class="{ active: $route.path === '/photo' }">Foto</button>
        </router-link>
      </div>
    </nav>
    <router-view></router-view>
  </div>
</template>


<script>
export default {
  name: 'App',
};
</script>

<style>
.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.hero-section {
  text-align: center;
  margin-bottom: 32px;
}

.hero-section h1 {
  font-size: 36px;
  margin-bottom: 16px;
}

.hero-section p {
  font-size: 20px;
  color: #e11111;
}

.content {
  margin-top: 20px;
  text-align: center;
}

.content ul {
  text-align: left;
  margin-top: 10px;
}

.content h3 {
  font-size: 24px;
  margin-bottom: 10px;
}

.content p {
  font-size: 16px;
  color: #1aca4f;
}

nav {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
}

.top-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f2f2; /* Optional: Set a background color for the buttons */
}

.bottom-buttons {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f2f2; /* Optional: Set a background color for the buttons */
}


nav button {
  background-color: rgb(61, 103, 60);
  color: white;
  border: none;
  border-radius: 4px;
  padding: 10px 20px;
  margin: 6px;
  font-size: 16px;
  transition: transform 0.3s ease, box-shadow 0.3s ease, background-color 0.3s ease;
}

nav button.active {
  background-color: #42c03d;
  transform: scale(1.1);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

nav button:hover {
  background-color: #42c03d;
  transform: translateY(-3px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
</style>
