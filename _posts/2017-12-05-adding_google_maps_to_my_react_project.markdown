---
layout: post
title:      "Adding Google Maps to my React project"
date:       2017-12-05 21:34:46 +0000
permalink:  adding_google_maps_to_my_react_project
---



For my [React project](https://github.com/Cecily2/travel-goals), I decided to build an app for users to keep track of their travel plans and goals. Users would be able to add trips with a location they wanted to visit, and add activities that they'd like to do for each of their trips. Since my idea was so focused on places, I thought from the beginning that it would be really cool to display them through a visual map. Ideally, I wanted there to be a separate /maps route that would show all a user's trips, with markers that you could click on to go to the trip's show page.

As I started to research how I might go about implementing this, I realized that there were actually two parts to what I wanted to do - first, getting coordinates based on the name of a location, and second, using those coordinates to render a map.

I found that the the [geocoder gem](http://www.rubygeocoder.com/) was an extremely simple and easy way to meet the first of these requirements. I could get it working just by adding latitude and longitude to my `trips` database table, and then adding these two lines to my Rails model:
```
    geocoded_by :location
    after_validation :geocode
```
The first line tells the gem to geocode the idem by the `location` column on my table, while the second line tells it to add the coordinates to the item as soon as it has been validated.

Now that each of my trips had coordinates, the next step was to hook up the Google Maps API with React and display the information. There are a lot of packages for Google maps/React integration, and I tried several before finding the functionality I wanted with the [react-google-map](https://www.npmjs.com/package/react-google-map) and [react-google-maps-loader](https://www.npmjs.com/package/react-google-maps-loader) packages.

Once these were installed, loading Google Maps was as simple as importing and calling the ReactGoogleMapLoader component with my API key. Within that, I called the ReactGoogleMap component with the details of what I wanted to display, something like this:

        <ReactGoogleMapLoader
            params={{
                key: GOOGLE_MAPS_KEY_HERE,
                libraries: "places,geometry",
            }}
            render={googleMaps =>
                googleMaps && (

                    <div className="map-container">
                        <ReactGoogleMap
                        googleMaps={googleMaps}
                        autoFitBounds={true}
                        coordinates={MAP_MARKER_COORDINATES_HERE}
                        />
                    </div>

                )}
            />

The MAP_MARKER_COORDINATES_HERE represent a list of coordinates for the map to put markers on. I also wanted an info window with certain information to pop up when these were clicked. Looking at the documentation, I figured out that I needed to pass it an array of objects with certain properties to represent each marker. So I ended up going through my trips list with `map` to get the properly-formatted list of marker information, like so:
```
const mapCoordinates = this.props.trips.map((trip) => {
    return {
        title: trip.location,
        position: {
            lat: trip.latitude,
            lng: trip.longitude
            },
        onLoaded: (googleMaps, map, marker) => {
                        const infoWindow = new googleMaps.InfoWindow({
                            content: `
                            <div class="map-item">
                                <h3><a href="/trips/${trip.id}">${trip.location}</a></h3>
                                // ...
                            </div>
                            `,
                        })
                        googleMaps.event.addListener(marker, "click", () => {
                            infoWindow.open(map, marker)
                        })
            }
    }
}
```

Once I added some styling, I ended up with a map page showing markers for each of a user's trips. Clicking a marker would bring up an info window with additional information and a link to that trip's page:

![](https://i.imgur.com/LaQtF0m.png)


And I decided I would also add a map to each trip show page, to make it easy for users to see the location of a specific trip:

![](https://i.imgur.com/rQeXUCB.png)

I was really happy to get everything working the way I wanted!

I know there are a lot of different ways to load an external API like Google Maps, so in the future I plan to research the other options and maybe refactor my code a bit. In particular, several articles I read suggested making the API call on the backend before returning the response to the client-side app. I wasn't able to figure out the details of how to do this in the time that I had to finish the app, but I'd love to come back to it later.
