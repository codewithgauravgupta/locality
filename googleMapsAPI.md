# Setup GCP Project:

https://console.cloud.google.com/welcome?pli=1

1. In the navigation bar, click the “Select a project” dropdown option to the left of the search bar.

2. Click the “NEW PROJECT” button in the top-right corner of the dialog box that appears.

3. On the next page under “Project name,” enter a name that best describes the project. Under “Location” select “No organization.” Then, click the “CREATE” button.

4. The GCP creates the project and returns to the “Welcome” page. Click the “SELECT PROJECT” button in the dialog box.

# Enable the project’s API:

The Maps Embed API and Maps JavaScript API must be enabled for this project. 

1. Navigate to “APIs & Services” -> library panel from the project dashboard. 

2. Click “VIEW ALL” under the “Maps” heading on the APIs library page.

3. Search “Maps Embed API” and “Maps JavaScript API,” and open either one of them.

4. Click the “Enable” button for the selected API to enable the API for the project. The site then redirects to the API overview page. A pop-up may appear asking to enable billing. Cancel this pop-up for now.

5. In the menu for “Additional APIs,” search for the second API.

6. Click the “Enable” button for the second API which enables the second API for this project. The site then returns to the API overview page.

# Create an API key:

we’ll use the API key to make API requests that don’t require user authorization. User authorization only identifies the application. It isn’t needed to access public resources anonymously.

1. Hover over the “APIs & Services” option, and click the “Credentials” option from the resulting menu.

2. Click “Create Credentials” -> “API key” option to create an API key.

3. Click the copy icon in front of the API key to copy it. Use this key for the Google Maps applications

# Setup Billing [Optional but has limited use without this step]

Sign in to the GCP, and go to the dashboard. Then, click the hamburger menu at the screen’s top-left corner.
In the hamburger menu, click the “Billing” button.
Click the “MANAGE BILLING ACCOUNTS” button to create the billing account.
On the“MANAGE BILLING ACCOUNTS” page, click the “ADD BILLING ACCOUNT” button.
From the resulting screen, select a country and what best describes your project needs from the dropdown menu. Then, accept the “Terms of Services,” and click “CONTINUE.”
Enter a phone number with the correct country code, and click the “SEND CODE” button.
The site asks for a code that has been sent to the phone number associated with the account. Enter that code to proceed.
Now, choose an account type, and fill in all the debit or credit card details on the “Payment method” form. Once the payment is registered successfully, Google creates a free trial account.

1. `Embed Maps on Web Pages`

The Maps Embed API embeds an interactive map in a web page using http but without JavaScript. Different map modes can be integrated based on specific use cases.

The Maps Embed API URL can simply be set as the src attribute of any iframe.

## Create a URL:

`https://www.google.com/maps/embed/v1/MAP_MODE?PARAMETERS&key=API_KEY`
	
Replace `MAP_MODE` with the map mode to be displayed.
Replace `PARAMETERS` with the required and optional parameters for the chosen map mode.
Replace `API_KEY` with the API key generated while setting up the credentials.

Map modes:
	
1. The `place` map mode will display a map focused on a particular address or place. The Google Maps API will highlight the focused location in red or place a marker on it.

e.g. 
`src="https://www.google.com/maps/embed/v1/place?q=Rome&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k"`

`src="https://www.google.com/maps/embed/v1/place?q=Taj+Mahal,Agra+India&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k"`

2. The `view` mode will display a map with no markers or directions. It won’t focus on any one place in particular.

e.g. 
`src="https://www.google.com/maps/embed/v1/view?center=40.689247,-74.044502&zoom=18&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k"`


3. The `directions` mode will display a route, distance, and travel time between two or more specified points.
The values Chicago+USA|Washington+DC+USA are passed to the waypoints pointer. This will display all the possible driving routes from Seattle to New York with stops in Chicago and Washington D.C.
e.g. `src="https://www.google.com/maps/embed/v1/directions?origin=Seattle+USA&destination=New+York+USA&waypoints=Chicago+USA|Washington+DC+USA&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k">`


4. The `streetview` mode displays Street View images as panoramic views from the specified locations–each panoramic view providing an interactive 360-degree view. The images have a 360-degree horizontal view and a 180-degree vertical view.
e.g. `src="https://www.google.com/maps/embed/v1/streetview?location=40.689247,-74.0445025&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k">`


5. The `search` mode displays the results of a search across a map. It requires the q parameter, which defines the search term.


## Add a URL in an iframe:

```html
<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1">

		<title>Maps Embed API</title>
		<meta name="description" content="Integration of Maps Embed API">
		<meta name="author" content="Educative">
	</head>

	<body>
		<iframe
			width="900"
			height="450"
			frameborder="0" style="border:0"
			loading="lazy"
			allowfullscreen
			src="https://www.google.com/maps/embed/v1/place?q=Rome&key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k">
		</iframe>
	</body>
</html>
```

2. `Create a Simple Map Using JavaScript`

To customize maps with images and shapes, it’s better to use coding in JavaScript instead of simply embedding the maps into web pages. To accomplish this task, we use the Google Maps JavaScript API.

The Map object: A map is represented using the google.maps.Map JS class. Objects of this class define a single map on a page. To create a new instance of this class, use JavaScript’s new operator.

It’s possible to create more than one instance of this class, in which each instance defines a separate map on the web page.

```html
<!DOCTYPE html>
<html>

<head>
    <title>Simple Map</title>
    <script src="https://polyfill.io/v3/polyfill.min.js?features=default"></script>
    <style>
        /* Always set the map height explicitly to define the size of the div 
   element that contains the map. */
        #map {
            height: 100%;
            width: 100%;
            /* height: 500px; */
        }

        /* Optional: Makes the sample page fill the window. */
        html,
        body {
            height: 100%;
            margin: 0;
            padding: 0;
        }
    </style>
    <script>
        let map;
        // var map;

        function initMap() {
            var uluru = { lat: 23.8388, lng: 78.7378 };
            map = new google.maps.Map(document.getElementById("map"), {
                center: uluru, // Coordinates of Seattle
                zoom: 8,
            });
        }
    </script>
</head>

<body>
    <div id="map"></div>
    <div id="info-box">?</div>

    <script async defer src="https://maps.googleapis.com/maps/api/js?
					callback=initMap&
					v=weekly&
					key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k"></script>
</body>

</html>
```

## Map Localization:

We can customize a map for a specific country or region by changing its default language settings or specifying a region code. This changes the map’s behavior based on the country.

`https://maps.googleapis.com/maps/api/js?
	callback=initMap&
	language=zh&
	region=CN&
	key=AIzaSyDMXp-2unkZGEGQveWZ4TR7sMlrOfssO1k"`


## Map Types:

Map types can be modified by using the mapTypeId property in the mapTypeId object or dynamically modified using the map.setMapTypeId() method.

These are the four basic types of maps in the Google Maps API:

1. `roadmap`: The roadmap type displays the default 2D map type, which is a normal road map. To use it, set the mapTypeId as roadmap.

2. `satellite`: The satellite type displays satellite imagery from Google Earth on the map. To use it, set the mapTypeId as satellite.

3. `hybrid`: The hybrid type displays a mix of satellite imagery and the standard road map view. To use it, set the mapTypeId as hybrid.

4. `terrain`: The terrain type uses terrain data to display a physical map with mountains, lakes, and more. To use it, set the mapTypeId as terrain.


## Tilted Map View:

`Rotated 45° imagery`: The satellite and hybrid map types also feature 45° imagery support. This is only available on zoom levels greater than 12. This high-resolution imagery provides perspective views towards any of the four principal compass directions.

When a user zooms onto a particular map section, the rotate control becomes visible, and a 45° perspective imagery replaces default imagery.

We can adjust 45° imagery behavior by adjusting the zoom level and the tilt level:

1. At zoom levels between 12 and 18, the 0° base map is displayed by default unless the tilt value is set to 45°.
2. At zoom levels greater than 18, the 45° base map is displayed by default unless the tilt value is set to 0°.

## Map Controls and the Default UI and Custom Controls:

When using the Google Maps JS API, several UI elements allow the user to control certain aspects of the map. For this reason, these UI elements are sometimes referred to as controls.

It’s also important to note that all default controls disappear if the map is smaller than 200 by 200 pixels. However, there is a way to override this behavior by explicitly setting these controls to be visible.


## Restrict Map Bounds:

Sometimes, there may be a need to restrict gesture and zoom controls to a certain part of the map. The Google Maps API has a number of properties that can be modified to enforce this restriction.

To restrict controls to a particular bound or set a maximum or minimum value of zoom, use the restriction, minZoom, and maxZoom options.

## Simple Events and Access Arguments in UI Events:

how to handle simple events on a map using event listeners.

There are two types of UI events, which are as follows:

1. State change events reflect changes in certain Maps JavaScript API objects. When an object’s property changes, an event is fired that states that the property has changed. For example, a zoom_changed event will be fired when the map’s zoom level changes.

2. User events are propagated from the DOM to the Maps JavaScript API. An example is a mouse click event.

Within the Maps JavaScript API, UI events can pass event arguments that can be accessed through an event listener. These event arguments can be accessed with an event listener in the same way the properties of JavaScript objects are accessed.

For example, the click event is a UI event that passes the MouseEvent argument to the event listener. One property that the MouseEvent argument includes is latLng, which denotes the precise location where the map is clicked.

The behavior mentioned above is unique to UI events since events related to state change don’t pass arguments.

e.g. An excellent example of applications that benefit from accessing latLng coordinates would be a ride-hailing applications like Uber. In ride-hailing applications, the user clicks on the map to drop their pick-up and drop-off location pins. The app then sends the coordinates of these pins and displays the corresponding markers on the assigned driver’s application.


## Drawing on Maps:

overview of drawing and adding overlay objects to a map that can highlight points, lines, or areas.

The Maps JavaScript API allows us to add objects to a map so that points, lines, or areas can be identified. These objects are called overlays and are tied to the latitude and longitude coordinates.

Overlays are a good way to customize a map and add interactivity to it. Overlays are tied to the latitude and longitude coordinates, so they move whenever zooming or dragging occurs on the map.

`Marker`:  Displays a single location on a map. Markers make it possible to identify locations on a map. They are an excellent way to highlight important places by setting custom icons. We use the `google.maps.Marker` constructor to add a marker. It takes an object that specifies the initial marker properties as input. The Marker constructor takes in the MarkerOptions parameter. This parameter defines the LatLng coordinates for its position and alters the marker’s visual features with a style set.

`Marker Customization`: We can have custom images.

`Marker labels`: label: "A",

`Cluster Markers`: Sometimes, it becomes incredibly messy when using a large number of markers, especially when zooming out on a map. To counter this issue, we can use the marker clusters to display many markers from a particular region concentrated in one place on the map. Then, as the cluster region is zoomed in on, the individual markers can be seen. Google’s markerclusterer library#
Use the googlemaps/markerclusterer library in combination with Maps JS API to cluster our markers. That’s the easiest way to detect markers and combine those that are close to each other into marker clusters.

We can use the following commands to add the markerclusterer library to the system with NPM or CDN:

npm install @googlemaps/markerclusterer
<script src="https://unpkg.com/@googlemaps/markerclusterer/dist/index.min.js"></script>

`Info Window`: Displays content, usually text or images, within a popup at a given location on a map. An InfoWindow object adds a popup window over the map at a given location and is used to display content. The info window has a content area and a tapered stem with the tip attached to some specific location on the map. An info window is usually attached to a marker or to some specific latitude and longitude.

`Polyline`: Displays lines on the map to represent an ordered sequence of locations. The Polyline object is used to draw connected lines on a map. It defines a linear overlay of line segments connected on the map. A Polyline is a list of LatLng locations on which line segments are drawn in an ordered sequence. They’re an excellent way to highlight paths or routes between specific points.

`Polygon`: Displays areas of arbitrary shapes on a map. Polygons represent a two-dimensional plane enclosed by a closed path where a series of coordinates define the enclosed path. A polygon has at least three sides. A Polygon object is drawn with a stroke and a fill. We can define custom style options for the stroke and custom colors for the enclosed area of the polygon.

A polygon’s area may consist of several separate paths. Therefore, the Polygon object’s path property specifies an array of arrays, and in each array, we specify a distinct sequence of ordered LatLng coordinates.

`Polygon with a hole`: we render a polygon over the Pentagon in Washington, DC, and create a hole over the open area in the middle of the Pentagon. To create an empty area within a polygon, we need to create two paths, one inside the other. To add these two paths to the Polygon object, we must pass an array of arrays of LatLng values to the paths parameters.

`Circle and Recatngle`: Display circle and rectangle objects on a map.

The Google Maps JavaScript API includes a specific Circle class that makes it easier to create and maintain circles on the map.

# Plus codes:

(https://support.google.com/maps/answer/7047426?hl=en-GB&co=GENIE.Platform%3DAndroid)

We can define Plus Codes are defined as digital addresses for a specific point on the map. Plus Codes exist as letters and numbers, and since we base them on latitude and longitude coordinates, we can use them even to locate places that do not have a physical address. For example, MXQ4+P66 New York, USA is the Plus Code for the Statue of Liberty. 



# URL-encoded addresses:

While passing values to a URL, there are some characters like spaces that we cannot use. When passing addresses to the Maps API URL, we encode such characters with other URL-friendly special characters to deal with this issue, like replacing spaces with either %20 or the plus sign, +.

Let’s take the address of the Eiffel Tower in Paris, "Eiffel Tower,Paris France", as an example. The URL-encoded address for this would be "Eiffel+Tower,Paris+France".

