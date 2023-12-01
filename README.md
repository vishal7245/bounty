# Player Markers Documentation

## Screenshot
![Screenshot](https://github.com/vishal7245/bounty/blob/main/Screenshot%20from%202023-12-01%2016-01-30.png)
![Screenshot2](https://github.com/vishal7245/bounty/blob/main/Screenshot%20from%202023-12-01%2016-10-43.png)

## Introduction
The `player.markers` function is used to enhance a player interface with markers, allowing users to mark specific points in a media player's timeline. This documentation will guide you through using this code snippet to add and customize markers in your web application.

## Prerequisites
Before implementing this code, make sure you have the following:

- video,js marker plugin
  ```git clone git@github.com:spchuang/videojs-markers.git```
- jQuery library included in your project.

## Usage

### Including Dependencies
Ensure that you have included the jQuery library in your HTML file:

```html
<script src="https://code.jquery.com/jquery-3.6.4.min.js"></script>
```

### Adding the Player Markers

```javascript
player.markers({
    // Customizing marker style
    markerStyle: {
        'width': '8px',
        'height': '4px',
        'background-color': '#acacb1',
    },

    // Adding the markers
    markers: section_markers,

    // Marker Tooltip configuration
    markerTip: {
        display: true,
        text: function (marker) {
            return marker.text;
        },
    },

    // Break overlay configuration
    breakOverlay: {
        display: true,
        displayTime: 3,
        text: function (marker) {
            return "This is an overlay: " + marker.text;
        }
    },

    // Event handler when a marker is reached
    onMarkerReached: function (marker) {
        console.log(marker);

        // Remove previous active class
        $("#marker-list li").removeClass("active");

        // Add active class to the current marker's button
        $("#marker-list li[data-index='" + marker.index + "']").addClass("active");
    },
});
```

### Marker List Setup

```javascript
$(document).ready(function () {
    // Insert marker list
    for (var i = 0; i < section_markers.length; i++) {
        var item = $("<li data-index='" + i + "'><a href='#'>" + section_markers[i].text + "</a></li>");
        $("#marker-list").append(item);
    }

    // Set up click event
    $("#marker-list li").click(function () {
        var index = $(this).data("index");

        // Set the player's current time to the selected marker's time
        player.currentTime(section_markers[index].time);
    });
});
```

## Customization

### Marker Style
You can customize the appearance of the markers using the `markerStyle` object. Adjust the properties such as `width`, `height`, and `background-color` to suit your design preferences.

### Tooltip
Configure the marker tooltip using the `markerTip` object. Set `display` to `true` if you want to show tooltips. Customize the displayed text using the provided function.

### Break Overlay
Customize the break overlay, which is displayed when a marker is reached, using the `breakOverlay` object. Adjust properties like `displayTime` and customize the overlay text.

### Marker List
You can customize the marker list's appearance and behavior by modifying the related code. Update the HTML structure, styling, and event handling to match your application's design.
