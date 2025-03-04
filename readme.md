<!DOCTYPE html>
<html>

<head>
	<meta charset=utf-8 />
	<title>Map Template Browser Title</title>
	<meta name='viewport' content='initial-scale=1,maximum-scale=1,user-scalable=no' />

	<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/normalize/5.0.0/normalize.css" />
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.0.1/dist/leaflet.css" />
	<link href="https://fonts.googleapis.com/css?family=Noto+Sans" rel="stylesheet">
	<link href="https://fonts.googleapis.com/css?family=Lora" rel="stylesheet">

	<style>
        <!--CSS-->
		body {
			margin: 0;
			padding: 0;
			background: "whitesmoke";
			font-family: "Noto Sans", sans-serif;
			color: #3d3d3d;
		}

		h1 {
			position: absolute;
			margin-top: 0;
			top: 10px;
			left: 45px;
			font-size: 2em;
			font-family: "Lora", serif;
			letter-spacing: .04em;
			padding: 10px 15px;
			background: rgba(256, 256, 256);
			border: 1px solid grey;
			border-radius: 3px;
			z-index: 800;
		}

		h2 {
			font-family: "Lora", serif;
			letter-spacing: .04em;
		}

		#map {
			position: absolute;
			top: 0;
			bottom: 0;
			width: 100%;
		}

		section {
			position: absolute;
			bottom: 0;
			left: 10px;
			width: 450px;
			margin: 20px auto;
			padding: 0 15px;
			background: rgba(256, 256, 256);
			border: 1px solid grey;
			border-radius: 3px;
			z-index: 800;
		}

		p {
			font-size: .9em;
			line-height: 1.5em;
		}

		a {
			color: #005daa;
			text-decoration: none;
		}

		a:hover {
			text-decoration: underline;
		}
	</style>
</head>

<body>

	<h1>Flat Top Tower Trail on the Blue Ridge Parkway</h1>

	<div id='map'></div>

	<section>
		<h2>Let's Go Hiking!<span style='font-size:28px;'>&#127748;</span></h2>

		<p>Discover this 5.1-mile out-and-back trail near Blowing Rock, North Carolina. Generally considered a moderately challenging route, it takes an average of 2 h 5 min to complete. This is a very popular area for hiking, horseback riding, and running, so you'll likely encounter other people while exploring. The trail is open year-round and is beautiful to visit anytime. Dogs are welcome, but must be on a leash.</p>
		

		<p>Enjoy this fairly easy trail that takes visitors along a few switchbacks, through meadows, and to an observation tower. The trail begins at Moses Cone Manor and travels along a wide gravel path. There is a short detour to Cone Cemetery for those who enjoy the history of this area. The trail then switchbacks through the forest to the summit with two decent overlooks along the way. Once you reach the top, you will find the fire tower, which offers beautiful 360-degree views.</p> 


		<p>Text provided by <a href="https://www.alltrails.com/trail/us/north-carolina/flat-top-mountain-trail">AllTrails</a></p>
		<p>More Information about Blue Ridge Parkway Trails<a href="https://home.nps.gov/blri/planyourvisit/moses-cone-trails.htm"> here!</a></p>
		<p>Map Authored By: Bridget Barr</p>

	</section>

	<script src="http://code.jquery.com/jquery-3.1.1.min.js"></script>
	<script src="https://unpkg.com/leaflet@1.0.1/dist/leaflet.js"></script>

    <script src ="data/route5.js"></script>

	<script>

           // console.log(data); (example to put in console in developer tools to make sure everything is working properly)
//options to be used when creating the map
		var options = {
			center: [36.159252, -81.691187],
			zoom: 15
		}

//creation of the Leaflet map
		var map = L.map('map', options);

//request to load basemap
var Esri_WorldTopoMap = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Topo_Map/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Esri, DeLorme, NAVTEQ, TomTom, Intermap, iPC, USGS, FAO, NPS, NRCAN, GeoBase, Kadaster NL, Ordnance Survey, Esri Japan, METI, Esri China (Hong Kong), and the GIS User Community'
}).addTo(map);

//var Thunderforest_OpenCycleMap = L.tileLayer('https://{s}.tile.thunderforest.com/cycle/{z}/{x}/{y}.png?apikey={apikey}', {
	//attribution: 'Tiles &copy; <a href="http://www.thunderforest.com/">Thunderforest</a>, &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
	//apikey: '<your apikey>',
	//maxZoom: 22
//}).addTo(map); 

//string content to be inserted into a tooltip
		//var message = 'Beacon Heights!';

//create a Leaflet marker, centered on the map's center.
	//	L.marker(map.getCenter())
		//	.bindTooltip(message) //bind the tooltip and message to the marker
		//	.addTo(map) // add the marker to the map`
		//	.openTooltip(); // open the tooltip

    //var myRoute = L.geoJson(data).addTo(map); 
    //map.fitBounds(myRoute.getBounds()); 
	//  (how to add geoJson route)

    var myRoute = L.geoJson(data, {
        filter : function(feature) {
           if(feature.geometry.type =="LineString") {
           return feature;
    }
        },
        style : function(feature) {
        return {
        color: "#0066cc",
        // the color is the six digit hex code, simple way to choose color
        weight: 6,
        opacity: 0.75,
        dashArray: "5, 12"
    }
    }
        }).addTo(map);


        var myStops = L.geoJson(data, {
       filter : function(feature) {
        if(feature.geometry.type == "Point") {
        return feature;
    }
   },
    

        onEachFeature : function (feature, layer) {
       // console.log(feature.properties)
       layer.bindTooltip(feature.properties['name']);
// attribute field name is 'name' for all of my points selected on map 
    }
        }).addTo(map);


	</script>

</body>
<!--Strava routes can be downloaded as a GPX file!!-->
</html>
