angular-video-background in a div
=================================

> html5 fullscreen video background in angular

[![Build Status](https://travis-ci.org/2013gang/angular-video-background.svg?branch=master)](https://travis-ci.org/2013gang/angular-video-background)

## Description

Eye-catching fullscreen video background is adopted by many modern websites for telling their stories. If you want to tell your own story in angular, you now have a choice. Just provide the video resouces, you can have your stunning video background right away.

## Demo
<a href="https://gang-demo.herokuapp.com/demo" target="_blank">you can see a demo here :)</a>

## Dependency
+ angular (*)

## How to get it

```bower install --save angular-video-background```

or

```npm install --save angular-vidbg```

## Usage

include 3rd dependencies (angular, lodash) and dist/vidBg.js in your js file

include dist/vidBg.css in your css file

then:

```html
<vid-bg resources="resources" poster="poster" full-screen="fullScreen" muted="muted" z-index="zIndex" play-info="playInfo" pause-play="pausePlay"></vid-bg>
```
```js
angular
	.module('demo', ['ngVidBg'])
	.controller('mainCtrl', ['$scope', function ($scope) {
		$scope.resources = [
			'http://techslides.com/demos/sample-videos/small.webm',
			'*.ogv',
			'*.mp4',
			'*.swf'
		];
		$scope.poster = 'http://placehold.it/2000&text=you%20may%20want%20to%20have%20a%20poster';
		$scope.fullScreen = true;
		$scope.muted = true;
		$scope.zIndex = '22';
		$scope.playInfo = {};
		$scope.pausePlay = true;
	}]);
```
Note: .webm, .ogv, .mp4 are the supported resource types. .swf is the fallback resource for environment that does not support the above types.

## options

| attribute         | optional? | example              | description                     		   |
|-------------------|-----------|----------------------|---------------------------------------------------|
| resources         | no        | ['xx.webm','yy.mp4'] | video resources                 		   |
| poster            | yes       | 'zzz.jpg'            | image shown before video loaded 		   |
| full-screen       | yes       | true                 | video will fill the width of its container        |
| pause             | yes       | false                | whether to pause the video                        |

there are a few other configurable options you may also want to use:
`muted`, `control`, `loop`, `auto-play`, `z-index`, `error-msg`

### Features
+ Dynamic change video resources and pause video
+ Show video buffer status and played status

## Coming soon
+ <strike>dynamic video change</strike>
+ <strike>detailed accessible information about your video including loading status, played range, etc.</strike>
+ testing on different browsers/devices
+ how to deal with legacy browsers and mobile

### Credits
  Inspired by <a href="http://demosthenes.info/blog/777/Create-Fullscreen-HTML5-Page-Background-Video" target="_blank">this</a>

  references: <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Using_HTML5_audio_and_video" target="_blank">[1]</a>, <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/video" target="_blank">[2]</a>, <a href="http://diveintohtml5.info/video.html" target="_blank">[3]</a>

### License
  MIT

#### Ref
http://stackoverflow.com/questions/33571027/how-to-play-local-video-in-ionic-app-video-tag-is-not-working

https://github.com/santoshshinde2012/FullscreenVideo

http://jsfiddle.net/P2NpU/31/

http://www.codeproject.com/Articles/113831/An-Advanced-Splash-Screen-for-Android-App


http://www.williammalone.com/articles/create-html5-canvas-javascript-sprite-animation/


https://www.kirupa.com/html5/sprite_sheet_animations_using_only_css.htm

http://blog.teamtreehouse.com/css-sprite-sheet-animations-steps

---------------------
csv
https://github.com/MounirMesselmeni/html-fileapi


with map--->

<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="initial-scale=1.0, user-scalable=no">
    <meta charset="utf-8">
    <title></title>
    <style>
      html, body {
        height: 100%;
        margin: 0;
        padding: 0;
      }
      #map {
        height: 100%;
      }
    </style>
  </head>
  <body>
    <div id="map"></div>
	
    <script>

      function initMap() {
		
		handleFiles("c:\app\Projects\test.csv");
	  
        var myLatLng = {lat: -40.363, lng: 53.044};
		var geocoder = new google.maps.Geocoder();
        var map = new google.maps.Map(document.getElementById('map'), {
          zoom: 3
        });

		var marker = new google.maps.Marker({
          position: geocodeAddress(geocoder, map),
          map: map,
          title: 'Hello World!'
        });
      }
	  
	function geocodeAddress(geocoder, resultsMap) {
	  var address = "98122, Calfornia, CA 098121";
	  geocoder.geocode({'address': address}, function(results, status) {
		if (status === google.maps.GeocoderStatus.OK) {
		  resultsMap.setCenter(results[0].geometry.location);
		  var marker = new google.maps.Marker({
			map: resultsMap,
			title: 'Hello World!',
			position: results[0].geometry.location
		  });
		} else {
		  alert('Geocode was not successful for the following reason: ' + status);
		}
	  });
	}
	
	
	function handleFiles(files) {
      // Check for the various File API support.
      if (window.FileReader) {
          // FileReader are supported.
          getAsText(files[0]);
      } else {
          alert('FileReader are not supported in this browser.');
      }
    }

    function getAsText(fileToRead) {
      var reader = new FileReader();
      // Read file into memory as UTF-8      
      reader.readAsText(fileToRead);
      // Handle errors load
      reader.onload = loadHandler;
      reader.onerror = errorHandler;
    }

    function loadHandler(event) {
      var csv = event.target.result;
      processData(csv);
    }

    function processData(csv) {
        var allTextLines = csv.split(/\r\n|\n/);
        var lines = [];
        for (var i=0; i<allTextLines.length; i++) {
            var data = allTextLines[i].split(';');
                var tarr = [];
				 for (var j=0; j<data.length; j++) {
                    tarr.push(data[j]);
                }
                lines.push(tarr);
        }
      console.log(lines);
    }

    function errorHandler(evt) {
      if(evt.target.error.name == "NotReadableError") {
          alert("Canno't read file !");
      }
    }
    </script>
    <!--script async defer
    src="https://maps.googleapis.com/maps/api/js?callback=initMap">
    </script-->
	<script type="text/javascript" src="readcsv.js"></script>
	
	 <input type="file" id="csvFileInput" onchange="handleFiles(this.files)"
          accept=".csv">
	 <div id="output">
    </div>
  </body>
</html>

