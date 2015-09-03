---
layout:     page
title:      The Biggest Number
date:       2014-03-06 15:32:15
summary:    A simple numbers game created for a school project using C# & WPF.
categories: Project
author:     Marvyn
thumbnail:  briefcase
tags:
 - C#
 - Project
---

<img class="thumbnail" src="{{ site.baseurl }}/projects/biggestNumber/images/BiggestNumber.jpg" alt="Biggest Number Screenshot">

# Summary
This was a simple game created for a school project where the user clicks on the largest number that is displayed on the screen.  This game was created on a 3x3 grid that generates 9 numbers labelled on buttons based on the bellow difficulty levels:

* Easy: Range 1-9
* Medium: Range 100-199
* Hard: Range 1000-9999

The user is timed and has one turn to select the biggest number on the grid for each round. If user is correct, their time and difficulty level is displayed.

### Game Board
The game board is split into 4 columns and 3 rows.  This allows areas for the top row to display the difficulty levels, timer information and scores heading.  The 3x3 Grid is put together using a dock panel, a uniformed grid, and is using the Grid.ColumnSpan element to stretch onto other columns to display properly.  The last row is reserved for user action buttons and the last column is reserved for displaying a list of user scores using a textblock.

### Game Start
By default the grid and grid buttons are disabled, so once the user clicks start, the grid and buttons becomes active, the difficulty level is checked, the numbers are generated using the random generator class and stored into an array.  These numbers are then displayed on the buttons in the grid by according to the button position, and the display timer is started.

### Gameplay Logic
When the user clicks on a button, the button location is compared the array position.  If the button is the same value as the maximum number in the array, the user is correct and time is reported along with difficulty level.  If the button is not the same value as maximum number in the array, the user is incorrect and round ends.

### Extras
* When user selects correct/incorrect button, all other buttons are turned off and corresponding button flashes green/green.
* Game will not start unless difficulty level is chosen (buttons remain turned off).
* Button to reset recorded scores.