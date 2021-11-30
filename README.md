# Objetos Multiparte
## A veces es necesario representar un mismo grupo de líneas o polígonos con exactamente las mismas características, o se requiere agrupar un mismo conjunto de geometrías dentro de una misma categoría, como lo hacemos cuando se trata de fallas normales e inversas, en efecto ambos elementos se tratan de líneas, pero se representan de manera diferente. 


Para todos estos casos, utilizamos objetos multiparte. Y para obtenerlo bastará con que coloquemos cada línea individual separada por comas como veremos a continuación.


``` html
<script>	
    var multiCoords2 = [
        [[20.9979327931889,-99.6000139878785],	[20.995125908942,-99.5973788300614],	[20.9926801382518,-99.5921213000854],	[20.9891781559809,-99.5868598122289],	[20.9825433691589,-99.5710915219616],	[20.9771064880642,-99.5652613786698],	[20.9718373894012,-99.561868434331],	[20.9644597883832,-99.5573435787267],	[20.9577915461491,-99.551135368615],	[20.9514738818929,-99.5453037232891],	[20.946213245972,-99.5391016275808],	[20.941656997154,-99.5327150983204],	[20.9327077317127,-99.5238780761574],	[20.9234002947527,-99.5169142540373],	[20.9184810341336,-99.5139000917154],	[20.9121631170992,-99.5076968958923],	[20.9047938286957,-99.4998048984395],	[20.8946186983336,-99.4881584922272],	[20.8839172999649,-99.4755755515579],	[20.8698797619327,-99.459613281919]],
        [[20.9864505473319,-99.6589094410503],	[20.965930372662,-99.6397997515034],	[20.944185005223,-99.6181608891656],	[20.92375936327,-99.5957841801346],	[20.9030675234594,-99.5731315657956],	[20.8778133000405,-99.5451310748095],	[20.8653165178023,-99.5310879847788],	[20.861678304098,-99.5265341469533],	[20.8558562815996,-99.5165426492398],	[20.853012656299,-99.5110090709012],	[20.841253635469,-99.4995011971166],	[20.8315334522226,-99.482525388088],	[20.8193283852707,-99.4724708431212],	[20.8070364380099,-99.461762483872],	[20.7999248478671,-99.4553765340919]],
        [[20.8314622682952,-99.7674744271168],	[20.8059873822925,-99.7570502711957],	[20.7961483888293,-99.7530705406783],	[20.787547843637,-99.7476001559792]],
        [[20.9665414720772,-99.8950189979251],	[20.9605811649254,-99.8904866045337],	[20.9565625159209,-99.8848418044195],	[20.9432619402968,-99.8701502421823],	[20.9365969062155,-99.8656154995197],	[20.9169520294459,-99.8522030231164],	[20.9018681111074,-99.8416289706003],	[20.8993285514064,-99.8390862880226],	[20.8948511192185,-99.8369075365438],	[20.8883478237276,-99.835092288143],	[20.8753452381665,-99.8306196053116],	[20.8665583670523,-99.8278560846098],	[20.8598942603818,-99.8228574908645],	[20.846542822916,-99.8176359661313],	[20.8322351269267,-99.8098828611938],	[20.8203704090243,-99.8065434189375],	[20.8009593001032,-99.7984851358953],	[20.7850617475465,-99.791757391533]]
    ];
 </script>
```

Posteriormente será necesario declarar un arreglo para añadir las caracteristics correspondientes, en este caso solamente hemos incluido el color negro, pero se pueden añadir muchas mas características


``` html
<script>
     var plArray = [];
    for(var i=0; i<multiCoords2.length; i++) {
        plArray.push(L.polyline(multiCoords2[i], {color:'black'}).addTo(map));
    }
</script>

```
### El código completo hasta ahora, se vería como algo así
``` html
<html>
<head>
	<meta charset="utf-8">
	<title>Mapa E14C17_2</title>
	<link rel="stylesheet" href="https://unpkg.com/leaflet@1.6.0/dist/leaflet.css"
  integrity="sha512-xwE/Az9zrjBIphAcBb3F6JVqxf46+CDLwfLMHloNu6KEQCAWi6HcDUbeOfBIptF7tcCzusKFjFw2yuvEpDL9wQ=="
  crossorigin=""/>
	<script src="https://unpkg.com/leaflet@1.6.0/dist/leaflet.js"
  integrity="sha512-gZwIG9x3wUXg2hdXF6+rVkLF/0Vi9U8D2Ntg4Ga5I5BZpVkVxlJWbSQtXPSiUTtC0TjtGOmxa1AJPuV0CPthew=="
  crossorigin=""></script>
	<style>
	#mapDIV {
	height: 100%;
	width: 100%;
	border: solid 2px black;
	}
	</style>
</head>
<body>
<div id="mapDIV"></div>

 <script>	
 var map = L.map('mapDIV', {
		center:[20.83748 , -99.71396],
		zoom:12
	});
	
	var scale = L.control.scale({
		'imperial':false
	});
	scale.addTo(map);
	
	var osm = L.tileLayer('http://a.tile.openstreetmap.org/{z}/{x}/{y}.png',
	{attribution: 'Map Data &copy; OpenStreetMap contributors'
	});
	osm.addTo(map);
	
	var topo = L.tileLayer('https://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
	maxZoom: 17,
	attribution: 'Map data: &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, <a href="http://viewfinderpanoramas.org">SRTM</a> | Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a> (<a href="https://creativecommons.org/licenses/by-sa/3.0/">CC-BY-SA</a>)'
	}); 
	topo.addTo(map);
	
	var sat = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
	attribution: 'Tiles &copy; Esri &mdash; Source: Esri, i-cubed, USDA, USGS, AEX, GeoEye, Getmapping, Aerogrid, IGN, IGP, UPR-EGP, and the GIS User Community'
	});

	
	var basemaps = {
		"OSM": osm,
		"Topografía": topo,										
		"Satélite": sat
		};
	L.control.layers(basemaps).addTo(map);
	
	
	var marcador1 = L.marker([20.83748 , -99.71396],{title:"Parada 1",alt:"",draggable:true}).addTo(map);


	var polyline1 = L.polyline([[20.8338559371212,  -99.783853949970251],	[20.82574053079675,  -99.782157466282968],	[20.818320593237736,  -99.779545644823031],	[20.81314155274011,  -99.778232293010518],	[20.808481817965063,  -99.776737886182715],	[20.803823725591378, -99.774875972833541],	[20.793302601443912,  -99.770043621075345],	[20.788819713020807,  -99.767631637171618],	[20.78329324063424,  -99.766684789579017],	[20.775524869070892,  -99.764624085463765],	[20.76689556449557,  -99.761824239652626]], {color: 'red',weight:2}).addTo(map);

	var polygon = L.polygon([[20.86114, -99.785305],[20.77543, -99.77069],[20.89791, -99.51015]], {color:'teal',weight:8}).addTo(map);

	var rectangle = L.rectangle([[20.74625, -99.94663],[20.765841, -99.94882]],
	 	{color: "red", 
	 	weight:8,
	 	fillColor:"blue"
		}
	).addTo(map);

	var circle = L.circle([20.89791, -99.51015], 10000,
		{color: "red",
		 weight:8,
		 fillColor:"blue"
		}
	).addTo(map);

    var multiCoords2 = [
        [[20.9979327931889,-99.6000139878785],	[20.995125908942,-99.5973788300614],	[20.9926801382518,-99.5921213000854],	[20.9891781559809,-99.5868598122289],	[20.9825433691589,-99.5710915219616],	[20.9771064880642,-99.5652613786698],	[20.9718373894012,-99.561868434331],	[20.9644597883832,-99.5573435787267],	[20.9577915461491,-99.551135368615],	[20.9514738818929,-99.5453037232891],	[20.946213245972,-99.5391016275808],	[20.941656997154,-99.5327150983204],	[20.9327077317127,-99.5238780761574],	[20.9234002947527,-99.5169142540373],	[20.9184810341336,-99.5139000917154],	[20.9121631170992,-99.5076968958923],	[20.9047938286957,-99.4998048984395],	[20.8946186983336,-99.4881584922272],	[20.8839172999649,-99.4755755515579],	[20.8698797619327,-99.459613281919]],
        [[20.9864505473319,-99.6589094410503],	[20.965930372662,-99.6397997515034],	[20.944185005223,-99.6181608891656],	[20.92375936327,-99.5957841801346],	[20.9030675234594,-99.5731315657956],	[20.8778133000405,-99.5451310748095],	[20.8653165178023,-99.5310879847788],	[20.861678304098,-99.5265341469533],	[20.8558562815996,-99.5165426492398],	[20.853012656299,-99.5110090709012],	[20.841253635469,-99.4995011971166],	[20.8315334522226,-99.482525388088],	[20.8193283852707,-99.4724708431212],	[20.8070364380099,-99.461762483872],	[20.7999248478671,-99.4553765340919]],
        [[20.8314622682952,-99.7674744271168],	[20.8059873822925,-99.7570502711957],	[20.7961483888293,-99.7530705406783],	[20.787547843637,-99.7476001559792]],
        [[20.9665414720772,-99.8950189979251],	[20.9605811649254,-99.8904866045337],	[20.9565625159209,-99.8848418044195],	[20.9432619402968,-99.8701502421823],	[20.9365969062155,-99.8656154995197],	[20.9169520294459,-99.8522030231164],	[20.9018681111074,-99.8416289706003],	[20.8993285514064,-99.8390862880226],	[20.8948511192185,-99.8369075365438],	[20.8883478237276,-99.835092288143],	[20.8753452381665,-99.8306196053116],	[20.8665583670523,-99.8278560846098],	[20.8598942603818,-99.8228574908645],	[20.846542822916,-99.8176359661313],	[20.8322351269267,-99.8098828611938],	[20.8203704090243,-99.8065434189375],	[20.8009593001032,-99.7984851358953],	[20.7850617475465,-99.791757391533]]
    ];
	

    var plArray = [];
    for(var i=0; i<multiCoords2.length; i++) {
        plArray.push(L.polyline(multiCoords2[i], {color:'black'}).addTo(map));
    }


	

	 
 </script>
</body>
</html>

```

### Al ejecutar en tu navegador deberías tener algo como esto.

![screenshot](https://raw.githubusercontent.com/sampach95/ObjetosMultiparte/master/img/multiparte.png )

Siguiente Tutorial https://github.com/IngGeolAsist/PopUps

Haz click en el siguiente enlace para volver a la pagina inicial
https://github.com/IngGeolAsist/ComoCrearMapasEnLaWebConLeaflet

