<template>
  <div class="location">
    <h1 class="location-header">Lokasi</h1>
    <div v-if="locationData">
      <p>Latitude: {{ locationData.latitude }}</p>
      <p>Longitude: {{ locationData.longitude }}</p>
      <p>Alamat: {{ locationData.address }}</p>
    </div>
    <div v-else>
      <p>Loading...</p>
    </div>
    <div id="map"></div>
    <button @click="fetchLocationData" class="btn-refresh">Refresh Lokasi</button>
  </div>
</template>


<script>
export default {
  name: 'Location',
  data() {
    return {
      locationData: null,
    };
  },
  mounted() {
    this.fetchLocationData();
  },
  methods: {
    async fetchLocationData() {
      try {
        if (navigator.geolocation) {
          const position = await new Promise((resolve, reject) => {
            navigator.geolocation.getCurrentPosition(resolve, reject);
          });
          const latitude = position.coords.latitude;
          const longitude = position.coords.longitude;

          const apiKey = '92591005a7b94008909d59a64b6d2a49';
          const apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${encodeURIComponent(
            latitude + ',' + longitude
          )}&key=${apiKey}`;

          const response = await fetch(apiUrl);
          const data = await response.json();

          this.locationData = {
            latitude,
            longitude,
            address: data.results[0].formatted,
          };

          this.displayMap(latitude, longitude);
        } else {
          console.error('Geolocation is not supported by this browser.');
        }
      } catch (error) {
        console.error('Error fetching location data:', error);
      }
    },
    displayMap(latitude, longitude) {
      const mapOptions = {
        center: { lat: latitude, lng: longitude },
        zoom: 10,
      };
      const mapElement = document.getElementById('map');
      const map = new google.maps.Map(mapElement, mapOptions);

      const marker = new google.maps.Marker({
        position: { lat: latitude, lng: longitude },
        map: map,
      });
    },
  },
};
</script>

<style>
.location {
  text-align: center;
  color: #fff;
  margin-top: 60px;
  position: relative;
}

.location::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/9d70ef73-ee0b-4abf-b97a-3389eff38ed5/d9qzqm8-242916ae-89d8-4da4-bfd4-93bef52e103a.gif?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7InBhdGgiOiJcL2ZcLzlkNzBlZjczLWVlMGItNGFiZi1iOTdhLTMzODllZmYzOGVkNVwvZDlxenFtOC0yNDI5MTZhZS04OWQ4LTRkYTQtYmZkNC05M2JlZjUyZTEwM2EuZ2lmIn1dXSwiYXVkIjpbInVybjpzZXJ2aWNlOmZpbGUuZG93bmxvYWQiXX0.DYvb7Sanh1SHlDEj6e748eHkUdk_Bjj8JB3CpmlHz8o'); 
  background-size: cover;
  background-position: center;
  opacity: 0.8;
  z-index: -1; /* Menempatkan latar belakang di belakang konten */
}


.location-header {
  margin-top: 20px;
  position: relative;
  z-index: 1;
  color: white;
}

.btn-refresh {
  padding: 10px 20px;
  background-color: rgb(61, 103, 60);
  color: #fff;
  border: none;
  cursor: pointer;
  position: relative;
  z-index: 1;
  margin-bottom: 60px;
}


.btn-refresh:hover {
  background-color: rgb(61, 103, 60);
}

#map {
  height: 80px;
  width: 100%;
  margin-top: 20px;
  position: relative; 
  z-index: 1;
}
</style>
