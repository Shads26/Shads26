<button onclick="changerTemperature(1)">+1°C</button>
<script>
  function getDHT11Data() {
      fetch('http://IP_DU_RASPBERRY:5000/dht11')
          .then(response => response.json())
          .then(data => {
              document.getElementById('temperature').innerText = data.temperature;
          });
  }
  setInterval(getDHT11Data, 5000);
</script>
