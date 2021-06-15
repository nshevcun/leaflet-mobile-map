<html lang="en">
<head>
<meta charset="utf-8">

<!-- The following script will the mobile browser to disable unwanted scaling of the page and set it to its actual size -->
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />

<!-- Step 1. Paste Leaflet CSS here -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
crossorigin=""/>

<!-- Step 2. Paste Leaflet JS here -->
<script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js" integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA==" crossorigin=""></script>

<style>
    /* These styles will help prepare the map for mobile view */
    body {
        padding: 0;
        margin: 0;
    }
    html, body, #map {
        height: 100%;
        width: 100vw;
    }

    /* Natalia's custom styles for easier viewing */
    .container {
        margin-left: 15px;
        margin-right: 15px;
        text-align: center;
    }

    .centerobject {
        display: block;
        margin-left: auto;
        margin-right: auto;
    }
  </style>

<title> Mobile Browser Map </title>
</head>

<body>
    <div class="container">
        <h1>Leaflet Map for Mobile Browsers</h1>
    </div>

    <div id="map" class="centerobject"></div>

  <!-- YOUR JAVASCRIPT HERE -->
  <script type="text/javascript">
    
    // Initialize the map showing the entire world (empty container)
    let map = L.map('map').fitWorld();

    // Populate the map window with the map
    L.tileLayer('https://tile.thunderforest.com/neighbourhood/{z}/{x}/{y}.png?apikey=e6af7839f94a43428e202e1290e0a2be', {
        attribution: 'Map data &copy; <a href="https://manage.thunderforest.com">Thunderforest</a> contributors, Imagery © <a href="https://manage.thunderforest.com/">Thunderforest</a>',
        maxZoom: 18,
        tileSize: 512,
        zoomOffset: -1,
        accessToken: 'e6af7839f94a43428e202e1290e0a2be'
    }).addTo(map);

    // Geolocation - Leaflet will automatically zoom the map to the detected location.
    // As soon as the user agrees to share his or her location and it’s detected by the browser, the map will set the view to it.
    map.locate({setView: true, maxZoom: 16});

    // Setting up a location marker through an event listener, showing accuracy in a popup:
    function onLocationFound(e) {
        let radius = e.accuracy;

        L.marker(e.latlng).addTo(map)
            .bindPopup(`You are within ${radius} meters from this point...`).openPopup();

        L.circle(e.latlng, radius).addTo(map);
    }

    map.on('locationfound', onLocationFound);

    // Generating an error if the geolocation fails:
    function onLocationError(e) {
        alert(e.message);
    }

    map.on('locationerror', onLocationError);

    // If you have setView option set to true and the geolocation failed, it will set the view to the whole world.
  </script>
</body>
</html>
