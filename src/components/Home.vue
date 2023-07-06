<template>
  <div class="home-container">
    <div class="hero-section">
      <h1>Halo! Selamat datang<br><span class="dannes-widget">Ini adalah project UAS Dannes (213510021)</span></h1>
    </div>
    <div class="content">
      <div class="feature-row">
        <ul>
          <li v-for="(feature, index) in features" :key="feature.title" class="feature-item" :class="{'bottom-row': index > 2}">
            <h3>{{ feature.title }}</h3>
            <p>{{ feature.description }}</p>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>




<script>
export default {
  data() {
    return {
      features: [
        {
          title: 'CUACA',
          description: 'Menampilkan cuaca sesuai dengan kota yang kamu cari.'
        },
        {
          title: 'LOKASI',
          description: 'Menampilkan lokasi rinci dengan sistem deteksi otomatis.'
        },
        {
          title: 'STOPWATCH',
          description: 'Fitur menampilkan timer.'
        },
        {
          title: 'GAME',
          description: 'Mainkan permainan sederhana batu gunting kertas!'
        },
        {
          title: 'Foto',
          description: 'Menampilkan album foto terbaik yang kamu punya.'
        }
      ]
    };
  }
};
</script>
  
<style scoped>
/* Gaya tambahan untuk font dan tata letak */
.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 200px;
}

.hero-section {
  text-align: center;
  margin-bottom: 2rem;
}

.hero-section h1 {
  font-size: 2.5rem;
  color: rgb(61, 103, 60);
  text-transform: uppercase;
  letter-spacing: 2px;
  margin-top: 70px;
  line-height: 1.5;
}

.dannes-widget {
  color: rgb(61, 103, 60);
  font-weight: bold;
}

ul {
  list-style-type: none;
  padding: 0;
}

.feature-item {
  margin-bottom: 1.5rem;
  padding: 1rem;
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease-in-out;
}

.feature-item:hover {
  transform: scale(1.05);
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.feature-item h3 {
  color: rgb(61, 103, 60);
  font-size: 1.3rem;
  margin-bottom: 0.5rem;
}

.feature-item p {
  color: #000000;
  font-size: 1rem;
}

.content {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.feature-row {
  flex: 1;
  max-width: 300px;
  margin: 1rem;
}

.bottom-row {
  margin-top: 2rem;
}

@media (max-width: 600px) {
  .feature-row {
    max-width: 100%;
  }
}
</style>
