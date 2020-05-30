# Secrets exploiting

## Tool

[Whitespots secrets hunter extension](https://addons.mozilla.org/en-US/firefox/addon/whitespots-dom-secrets-hunter/)

## Google Maps Key

```markup
<html>
<head>
<title>PoC JavaScript API</title>
<meta name="viewport" content="initial-scale=1.0"><meta charset="utf-8">
<style>
   #map { height: 100%; }
  html, body { height: 100%; margin: 0; padding: 0; }
</style>
</head>
  <body><div id="map"></div>
    <script>
      var map;
      function initMap() {
        map = new google.maps.Map(document.getElementById('map'), {
          center: { lat: -34.397, lng: 150.644 },
          zoom: 8
        });
      }
    </script>
    <script src="https://maps.googleapis.com/maps/api/js?key=<key_here>&callback=initMap"
    async defer></script>
  </body>
</html>

```

### Impact

$5000 per hour budget spending

### Fix

Referer header

## Yandex Maps Key

```markup
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title>Quick start. Placing an interactive map on a page</title>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <script src="https://api-maps.yandex.ru/2.1/?apikey=<key>&lang=en_US" type="text/javascript">
    </script>
    <script type="text/javascript">
        ymaps.ready(init);
        function init(){
            var myMap = new ymaps.Map('map', {
                center: [55.75, 37.57],
                zoom: 9,
                controls: ['routePanelControl']
            });
            var multiRoute = new ymaps.multiRouter.MultiRoute({
                // Точки маршрута. Точки могут быть заданы как координатами, так и адресом.
                referencePoints: [
                    'Москва, метро Смоленская',
                    'Москва, метро Арбатская',
                    [55.734876, 37.59308], // улица Льва Толстого.
                ]
            }, {
                  // Автоматически устанавливать границы карты так,
                  // чтобы маршрут был виден целиком.
                  boundsAutoApply: true
            });
            // Добавление маршрута на карту.
            myMap.geoObjects.add(multiRoute);
            myMap.geoObjects.add(multiRoute);
            myMap.geoObjects.add(multiRoute);
            myMap.geoObjects.add(multiRoute);
            // И так далее...
         }
    </script>
</head>

<body>
    <div id="map" style="width: 600px; height: 400px"></div>
</body>
</html>

```

### Impact

Money spending \(up to [tariff](https://tech.yandex.com/maps/commercial/doc/concepts/jsapi-geocoder-docpage/#jsapi-geocoder__tariffs)\)

### Fix

Referer header

