### Leaflet package:


```javascript
if (navigator.geolocation)
  navigator.geolocation.getCurrentPosition(
    function (position) {
      const { latitude } = position.coords;
      const { longitude } = position.coords;
      console.log(`https://www.google.pt/maps/@${latitude},${longitude}`);

      //   Leaflet map implemented
      const coords = [latitude, longitude];
      const map = L.map('map').setView(coords, 13);

      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(map);


// Created a marker in the map
      map.on('click', function (mapEvent) {
        const { lat, lng } = mapEvent.latlng;
        L.marker([lat, lng]).addTo(map).bindPopup('Workout').openPopup();
      });
    },
    function () {
      console.log("Can't access you location");
    }
  );
```
