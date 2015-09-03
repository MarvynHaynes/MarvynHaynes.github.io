---
layout:     page
title:      Sailboat Racing Analyzer
date:       2015-09-01 17:57:21
summary:    A Java application that replays sailboat positioning using GPS co-ordinates.
categories: Project
author:     Marvyn
thumbnail:  briefcase
addCSS:     myCustom.css
tags:
 - Java
 - Project
---

<img class="thumbnail" src="{{ site.baseurl }}/projects/sailboat/images/Sailboat_Analyzer.jpg" alt="Sailboat Analyzer">

# Overview

As part of my curriculum, I worked with a team of student developers to research and develop an application requested by a client.  Information was gathered through a series of interveiws and meetings that were conducted with the client and we were able to create deliveries and milestones up to the final project completion date for a prototype.  The client has requested that we use a private secure Git Repository for version control to ensure that the program source code is not freely available.

### Summary

The client wanted a Sailboat Racing App which will allow him to replay recorded sailboat movements during sailboat races. Additional features requested by the client included: ability to read KML data, markers that display each boat, playback functionality, smooth animation, map navigation and to be created on Java for multi-platform use.

### Data Design

Once the program starts, the user will use the open dialog to retrieve information via [KML (Keyhole Markup Language)](https://support.google.com/earth/answer/148118?hl=en) files that allows us to display geographical information that is used by geospatial software.  This is commonly used by applications such as Google Maps, Google Earth and various other tracking software that can display marks, images, and textual descriptions. For more info and tutorial, click here.

KML files are structured in [XML notation](http://www.w3schools.com/schema/el_notation.asp) and allows us to view and display data.  Some of the elements tags that were used for this project include:

<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_kml.jpg" alt="Sailboat KML">

* **gx:coord**  - consists of floating point values for longitude and latitude.
* **when** - tracks the exact time the gps co-ordinates was made.
* **Timestamp** - consists of time intervals for each set of data.
* **gx:Track** - contains information about the track co-ordinates.


### Sailboat List

<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_namelist.jpg" alt="Sailboat list" class="pull-right">

Once the user opens the KML file, The program reads the data and translate into tracks for a single boat.  The user is then prompted to enter a name for the boat, and the path is displayed on the map with the help of [PathTransitions](https://docs.oracle.com/javafx/2/api/javafx/animation/PathTransition.html).  The user can load as many tracks as they wish, and to avoid confusion, each boat is assigned a different color and track.  The boat list remains on the top left side of the GUI and the user has the option to add or remove the highlighted boat using JavaFX's [button EventListeners](http://docs.oracle.com/javafx/2/ui_controls/button.htm).


### Panning / Zooming

<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_mapButtons.jpg" alt="Sailboat Map Buttons" class="pull-left">

Similar to an interactive map style, the GUI contains panning and zooming buttons along with zooming in and out.  Each panning button was assigned a PanLeft, Right, Up, Down method which adds or subtracts a specific value from the [.getTranslateX](http://www.java2s.com/Tutorial/Java/java.awt.geom/AffineTransform/Java_AffineTransform_getTranslateX_.htm) and [.getTranslateY](http://www.java2s.com/Tutorials/Java/java.awt.geom/AffineTransform/Java_AffineTransform_getTranslateY_.htm) properties.  The zooming feature was accomplished by modifying the the [.setScaleX](https://docs.oracle.com/javafx/2/api/javafx/scene/Node.html#setScaleX%28double%29) and [.setScaleY](https://docs.oracle.com/javafx/2/api/javafx/scene/Node.html#setScaleY%28double%29) properties.


### Map Display

<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_map.jpg" alt="Sailboat Map">

With the use of Event listeners, we were able to create click and drag effects to navitgate movement along with mouse scroll for zooming in and out.  The same interaction was also created for touchpad use for users of laptops.  In both scenarios, this feature was implemented my tracking the initial X/Y co-ordinates of where the left button was first clicked and calculate the distance to where the button was released.  Some of the properties used to create these features were

* .setOnMousePressed()
* .setOnMouseDragged()
* ZoomEvent.ZOOM_STARTED
* ScrollEvent.SCROLL_STARTED
* .getDeltaY() (for mouse scroll value)


### Scale Legend
<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_scale.jpg" alt="Sailboat Scale">
As the user zooms in and out, the scale legend value changes to reflects the distance (in KM).  This feature was also added using EventListiners for Zooming functions.


### Playback Options

<img src="{{ site.baseurl }}/projects/sailboat/images/sailboat_playback.jpg" alt="Sailboat Playack Buttons" class="pull-right">

Again, using EventHandlers, we were able to implement playback features by manipulating the TransitionPath properties.  To assure each of the boat paths will respond to each type of play action at the same time, all boat paths were added into a group.  As shown above, the following features were added:

* Playback Speed (slider EventListener)
* Rewind (5 second increments)
* Restart
* Pause
* Play
* Fast Foward (5 second increments)
 