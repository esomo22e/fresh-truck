<script>
   import { onMount, afterUpdate } from "svelte"
   import mapboxgl from 'mapbox-gl'

  let mapRef;

  // props
  export let centerlnglat
  export let pitch
  export let bearing
  export let zoom
  export let data
  export let active

  let datapoints = []


   onMount(async () => {
      data.forEach(d => {
         let newobj = {
           "type": "Feature",
           "properties": {
             "title": d.name,
             "anchor": "right",
             "anchor-offset": [-1, 0]
           },
           "geometry": {
             "coordinates": [
               d.lng,
               d.lat
             ],
             "type": "Point"
           },
           "id": d.id
         }

         datapoints.push(newobj)

      })

      mapboxgl.accessToken = 'pk.eyJ1IjoidG1hY2hhZG9udSIsImEiOiJjanVjdDFudDMwMDR4NGRtdGJ4NndiaW9pIn0.JS0ffUQym0L07752GAwMFg';

     // Create the map
      mapRef = new mapboxgl.Map({
         container: 'map',
         style: 'mapbox://styles/tmachadonu/ckgic5tcc7iur19mynsutt5jh',
         center: centerlnglat,
         zoom: zoom,
         bearing: bearing,
         pitch: pitch
      });

      mapRef.on('load', function() {
         mapRef.addSource('points', {
            'type': 'geojson',
            'data': {
              "features": datapoints,
              "type": "FeatureCollection"
            }
         });

//          mapRef.addSource('route', {
// 'type': 'geojson',
// 'data': {
// 'type': 'Feature',
// 'properties': {},
// 'geometry': {
// 'type': 'LineString',
// 'coordinates': [
// [-71.069861929033, 42.32425619202166],
// [ -71.07037345035343,42.32435687967843],
// [ -71.06916680831134, 42.32505301355613],
// [ -71.07086904456389, 42.32629348273941],
// [ -71.06752399346762,42.32755182658471],
// [ -71.06959855812107,42.33004168702157],
// [-71.06798253968049,42.33147647040757],
// [ -71.07134960912913,42.33229788256198],
// [ -71.06865595357021,42.33481183492039],
// [ -71.06481753526843,42.335357341774944],
// [ -71.06298426409224, 42.34019709385547],
// [ -71.05975015548263, 42.3450967740915],
// [ -71.04950350179993,42.34760581574173],
// [ -71.04954321193173,42.347673881959544],
// [ -71.04944553157141, 42.34765830240937],
// [ -71.04631265680479, 42.34808708187328],
// [ -71.0451136553509,42.3482300077113],
// [ -71.03892526075018,42.34665780561976],
// [ -71.04054035073855,42.34703212961392],
// [ -71.03579808414543,42.34703212961392],
// [ -71.03192219317988,42.34922265819685],
// [ -71.02727112402124,42.35559160763826],
// [ -71.02583823212201,42.35813939958449],
// [ -71.02467538106116,42.36523333772184],
// [ -71.02920757130215,42.37416308187537],
// [ -71.02920757130215,42.37540946897192],
// [ -71.02478449655203,42.379653736779446],
// [ -71.02542287847473,42.37988952102435],
// [ -71.02649300236574, 42.37948649052785],
// [ -71.03446357398238, 42.3727396503911],
// [-71.0371, 42.3742]
// ]
// }
// }
// });
//
// mapRef.addLayer({
// 'id': 'route',
// 'type': 'line',
// 'source': 'route',
// 'layout': {
// 'line-join': 'round',
// 'line-cap': 'round'
// },
// 'paint': {
// 'line-color': 'red',
// 'line-width': 6
// }
// });
//
//
// mapRef.addSource('route2', {
// 'type': 'geojson',
// 'data': {
// 'type': 'Feature',
// 'properties': {},
// 'geometry': {
// 'type': 'LineString',
// 'coordinates': [
//     // [-71.0441,42.2867],
//     [-71.1371,42.277],
//     [ -71.1355562039911,42.27940960437894],
//     [-71.12791727292245,42.27432909559769],
//     [ -71.12353990792809,42.27813951558259],
//     [ -71.12001627062644,42.278660932694],
//     [ -71.11684499705493,42.27892163963178],
//     [ -71.09165099034804,42.296972971383994],
//     [ -71.08680208894329,42.2982109597993],
//     [ -71.08661810684825,42.29793879371979],
//     [ -71.08523824113541,42.30344992755704],
//     [ -71.07815493047622,42.30583113243702],
//     [ -71.07405242695017,42.30491990643264],
//     [-71.0677, 42.3059],
//     [ -71.06480830395344,42.30810286781362],
//      [-71.06382200297318,42.30810286781362],
//        [ -71.06267131849624,42.307464635205434],
//        [ -71.05806858058841,42.29925821095674],
//        [ -71.05745214247577,42.29877187076309],
//        [ -71.05667132086641,42.29770798849412],
//        [-71.05124666547505,42.293695470786695],
//        [ -71.04633830516904,42.28760396570849],
//        [ -71.04406769946499,42.28653796702176]
//
//     // [ -71.06480830395344,42.30801169212291],
//     // [ -71.06388560628062,42.30826580185285],
//     // [ -71.06496060374612,42.30797431464693],
//     // [ -71.06391693991148,42.308311081530704],
//     // [ -71.05850904886131,42.299746517740566],
//     // [ -71.05743313336443,42.29863659902105],
//     // [ -71.0567503560582,42.29782628391905],
//     // [ -71.05632133382092,42.29729062205684],
//     // [ -71.05126884623172,42.293477871161585],
//     // [ -71.04634639138132,42.28751993964204],
// // [-71.0677, 42.3059]
//
// ]
// }
// }
// });
//
// mapRef.addLayer({
// 'id': 'route2',
// 'type': 'line',
// 'source': 'route2',
// 'layout': {
// 'line-join': 'round',
// 'line-cap': 'round'
// },
// 'paint': {
// 'line-color': 'blue',
// 'line-width': 6
// }
// });
//
// mapRef.addSource('route3', {
// 'type': 'geojson',
// 'data': {
// 'type': 'Feature',
// 'properties': {},
// 'geometry': {
// 'type': 'LineString',
// 'coordinates': [
// [-71.0528,42.3333],
// [ -71.0559330296048,42.338683768274784],
// [ -71.05687716715262,42.33798588007488],
// [ -71.05533221480165,42.33709764752761],
// [ -71.05610469097712,42.336526634264956],
// [ -71.05258563284437,42.32942025770715],
// [ -71.05146983392423,42.32174193072717],
// [ -71.05146983392423,42.32174193072717],
// [ -71.04951661074374,42.300585235188876],
// [ -71.05573364481327,42.30429119368442],
// [ -71.05935251539107,42.30278138507349],
// [-71.0593,42.3044],
// [-71.05870297451813,42.3059382163305],
// [ -71.05870297451813, 42.3059382163305],
// [ -71.05870297451813,42.3059382163305],
// [ -71.06232184509592,42.30744794923715],
// [ -71.06408488460818,42.308751780337346],
// [ -71.06612629878026,42.30909488929631],
// [ -71.08292156992333,42.31629974541774],
// [ -71.08171527973073,42.31780922981137],
// [ -71.09182955903789,42.32178860601735],
// [ -71.09331422389032,42.320896698749735],
// [ -71.0953556380624,42.32192582139793],
// [ -71.09544842961567,42.32370959411393],
// [ -71.09758263534103,42.32480727526415],
// [ -71.10027359038607,42.32617934976984],
// [-71.09971684106641,42.32707118215142],
// [ -71.10899599639407,42.32974660343664],
// [ -71.10843924707441,42.33043259056534],
// [ -71.10936716260717,42.33317646426715],
// [-71.1097,42.3331]
// ]
// }
// }
// });
//
// mapRef.addLayer({
// 'id': 'route3',
// 'type': 'line',
// 'source': 'route3',
// 'layout': {
// 'line-join': 'round',
// 'line-cap': 'round'
// },
// 'paint': {
// 'line-color': 'purple',
// 'line-width': 6
// }
// });
//
// mapRef.addLayer({
// 'id': 'route2',
// 'type': 'line',
// 'source': 'route2',
// 'layout': {
// 'line-join': 'round',
// 'line-cap': 'round'
// },
// 'paint': {
// 'line-color': 'blue',
// 'line-width': 6
// }
// });
//
// mapRef.addSource('route4', {
// 'type': 'geojson',
// 'data': {
// 'type': 'Feature',
// 'properties': {},
// 'geometry': {
// 'type': 'LineString',
// 'coordinates': [
// [-71.0839,42.3128],
// [42.31142395722057, -71.08265216072445],
// [42.307234697096895, -71.07578570583127],
// [42.31256643432088, -71.06771762133178],
// [42.32027497514636, -71.0615054904572],
// [42.3280271694668, -71.05772904641599],
// [42.32799432320097, -71.0560851825392],
// [42.32683055710494, -71.05595421373732],
// [42.32687134824878, -71.05549902663252]
// [ -71.0547,42.3267],
// [-71.0602,42.3782]
//
// ]
// }
// }
// });
//
// mapRef.addLayer({
// 'id': 'route4',
// 'type': 'line',
// 'source': 'route4',
// 'layout': {
// 'line-join': 'round',
// 'line-cap': 'round'
// },
// 'paint': {
// 'line-color': 'orange',
// 'line-width': 6
// }
// });








         // mapRef.addLayer({
         //    'id': 'points-circles',
         //    'source': 'points',
         //    'type': 'circle',
         //    'paint': {
         //       'circle-radius': 4,
         //       'circle-color': 'blue',
         //       // 'circle-stroke-color': 'red',
         //       'circle-stroke-width': 4
         //    }
         // });





         datapoints.forEach(function(marker) {
             console.log(marker)

           // console.log(marker);
            let el = document.createElement('div');
            // console.log(el)
            el.className = 'marker';
            el.dataset.placeid = marker.id;




            console.log(el.outerHTML)


            if(marker.id === 1 || marker.id === 8 || marker.id === 6|| marker.id === 10){
              // el.style.backgroundImage = "url('//news.northeastern.edu/interactive/2020/10/campus-construction-2020/photos/" + marker.id + ".jpg')";

              // el.style.border = "3px solid black";
              //   el.style.width= "55px";
              //   el.style.height = "55px";


              // let span = document.createElement("span");
              // span.className = 'arrow';
              // el.appendChild(span);
              // span.dataset.placeid = marker.id;

// desc.style.display = "hidden";
  // var desc =  document.getElementById("map-cont");
  // desc.style.zIndex = 100;
        el.style.backgroundImage = "url('https://img.icons8.com/ios-filled/50/000000/marker.png')";
          el.style.width= "55px";
          el.style.height = "55px";


            }
            else if(marker.id === 19){
                el.style.backgroundImage = "url('https://img.icons8.com/officel/80/000000/marker.png')";
                el.style.width= "65px";
                el.style.height = "65px";
            }
            else{
              el.style.backgroundImage = "url('https://img.icons8.com/ultraviolet/40/000000/marker.png')";
              el.style.width= "55px";
              el.style.height = "55px";

              // el.style.backgroundImage = "url('//news.northeastern.edu/interactive/2020/10/campus-construction-2020/photos/" + marker.id + ".jpg')";
              var desc =  document.getElementById("map-cont");
              // desc.style.backgroundColor = "red";
              // desc.style.zIndex = 0;
            }
             // el.style.backgroundImage = "url('https://img.icons8.com/color/48/000000/marker--v1.png')";

            //
            el.addEventListener('click', function() {
               active = data.filter(d => (d.id === marker.id))[0];
               active = active
               activeChange(active)
            })
            //
            new mapboxgl.Marker(el)
             .setLngLat(marker.geometry.coordinates)
             .addTo(mapRef);

           //   new mapboxgl.Marker()
           // .setLngLat([40.6483, -74.0237])
           // .addTo(mapRef);

            //   new mapboxgl.Marker(el)
            // .setLngLat([42.3333, -71.08872])
            // .addTo(mapRef);
         });

         // mapRef.addLayer({
         //    'id': 'points-labels',
         //    'source': 'points',
         //    'type': 'symbol',
         //    'layout': {
         //       'icon-image': 'custom-marker',
         //       'text-field': [
         //       'format',
         //       ['get', 'title'],
         //       { 'font-scale': 1 }
         //       ],
         //       'text-font': [
         //          'DIN Offc Pro Medium',
         //          'Arial Unicode MS Bold'
         //       ],
         //       'text-offset': ['get', 'anchor-offset'],
         //       'text-anchor': ['get', 'anchor'],
         //       'text-justify': ['get', 'anchor']
         //    },
         //    "paint": {
         //        "text-color": "#202",
         //        "text-halo-color": "#fff",
         //        "text-halo-width": 3
         //    },
         // });

         // mapRef.on('click', 'points', function(e) {
         //    var coordinates = e.features[0].geometry.coordinates.slice();
         //    var description = e.features[0].properties.title;
         //
         //    // Ensure that if the map is zoomed out such that multiple
         //    // copies of the feature are visible, the popup appears
         //    // over the copy being pointed to.
         //    while (Math.abs(e.lngLat.lng - coordinates[0]) > 180) {
         //       coordinates[0] += e.lngLat.lng > coordinates[0] ? 360 : -360;
         //    }
         //
         //    new mapboxgl.Popup()
         //       .setLngLat(coordinates)
         //       .setHTML(description)
         //       .addTo(mapRef);
         // });

         // Change the cursor to a pointer when the mouse is over the places layer.
         // mapRef.on('mouseenter', 'places', function() {
         //    mapRef.getCanvas().style.cursor = 'pointer';
         // });
         //
         // // Change it back to a pointer when it leaves.
         // mapRef.on('mouseleave', 'places', function() {
         //    mapRef.getCanvas().style.cursor = '';
         // });

      })
   }); //onMount

   //GOOOO TO LOCATION

   afterUpdate(() =>
      activeChange(active)
   )
   //
   function activeChange(active) {
      // let prevactive = document.querySelector(".active");
      // let activeplace = document.querySelector("[data-placeid='" + active.id + "']");
      // if (prevactive) {
      //    prevactive.classList.remove("active")
      // }
      // if (activeplace) {
      //    activeplace.classList.add("active")
      // }

      // if (active.lng) {
      //    mapRef.flyTo({
      //       center: [
      //          active.lng - 0.00025,
      //          active.lat + 0.00012
      //       ],
      //       zoom: 18,
      //       essential: true
      //    });
      // }
	}
</script>



<style>

:global(.marker) {
    background-size:cover;
    /* color: red; */
    /* border:2px solid black; */
    width: 45px;
  height: 45px;
    border-radius: 50%;
    cursor: pointer;
    position: absolute;
     top: -36px;
     left: 0;
     will-change: transform;
    z-index: 1
  }
 /* :global(.marker) {
     background-size:cover;
     color: red;
     border:2px solid black;
     width: 75px;
     height: 75px;
     border-radius: 50%;
     cursor: pointer;
     position: absolute;
      top: -36px;
      left: 0;
      will-change: transform;
     z-index: 1
   } */



      /* :global(.marker.active) {
     width: 220px;
     height: 220px;
     top: -110px;
     z-index:50
   } */
   :global(span.arrow) {
  /* width: 45px; */
  /* height: 45px; */
  /* top: -23px; */
  z-index:50
}
   /* At the bottom of the tooltip */

   :global(span.arrow) {
     content: " ";
     position: absolute;
     top: 100%;
     left: 50%;
     margin-left: -10px;
     border-width: 10px;
    /* border-height:100px; */
     border-style: solid;
     border-color: black transparent transparent transparent;
   }

   :global(.mapboxgl-control-container div) {
      display:inline-block;
   }

   :global(.mapboxgl-control-container) {
      display:inline-block;
      position:relative;
      top: -40px;
      height: 40px;
      background-color:rgba(255, 255, 255, 0.8);
   }

   :global(.mapboxgl-control-container a) {
      color:#555;
      font-size:10px;
      margin-right:0.5rem;
   }

   #map {
      position: absolute;
      top: 0;
      bottom: 0;
      width: 100%;
      height: 100vh;
  }

  @media screen and (min-width:600px) {
     :global(.marker.active) {
      width: 300px;
      height: 300px;
      top: -150px;
      z-index:50
     }
  }

</style>

<div id="map"></div>
