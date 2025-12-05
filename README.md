# Mini-App
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Location Mini App</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; padding: 50px; }
    button { padding: 10px 20px; font-size: 16px; cursor: pointer; }
  </style>
</head>
<body>
  <h2>Mini App: Share Your Location</h2>
  <p>Click below to share your location:</p>
  <button onclick="getLocation()">Share Location</button>
  <p id="status"></p>
  <p id="coords"></p>

  <script>
    function getLocation() {
      const status = document.getElementById('status');
      const coords = document.getElementById('coords');
      status.textContent = '';
      coords.textContent = '';

      if (!navigator.geolocation) {
        status.textContent = 'Geolocation is not supported by your browser.';
        return;
      }
      
      status.textContent = 'Locating...';

      navigator.geolocation.getCurrentPosition(
        (position) => {
          status.textContent = 'Location found!';
          coords.innerHTML = 
            `Latitude: ${position.coords.latitude}<br>Longitude: ${position.coords.longitude}`;
        },
        (error) => {
          switch(error.code) {
            case error.PERMISSION_DENIED:
              status.textContent = 'Permission denied. Please allow access to your location.';
              break;
            case error.POSITION_UNAVAILABLE:
              status.textContent = 'Location information is unavailable.';
              break;
            case error.TIMEOUT:
              status.textContent = 'Location request timed out.';
              break;
            default:
              status.textContent = 'An unknown error occurred.';
          }
        }
      );
    }
  </script>
</body>
</html>
