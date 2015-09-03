---
layout:     page
title:      Cigarette Savings Calculator
date:       2014-01-23 16:43:12
summary:    A school assignment that calculates money saved per cigerette.
categories: Project
author:     Marvyn
thumbnail:  briefcase
tags:
 - HTML
 - PHP
 - Javascript
 - Project
---

<img class="thumbnail" src="{{ site.baseurl }}/projects/ciggCalc/images/onlineCigg.JPG" alt="Ciggerette Money Saver Calculator Screenshot">

This was a project I created for one of my Web Programming assignments which required the following:

* Duplicate the visual layout of the form in HTML using a printout that was provided
* Using Javascript, validate form inputs
* Calculate savings earned based from the inputs of price per pack, ciggerettes per pack, number of ciggerattes smoked per day and current date
* Data is then entered to a database using PHP

Things to note:

* While the original website was fully functional and connected to a database, this demonstration I opted to display the PHP commands that would of been sent to the database.
* Each input field displays error messages accordingly
* The javascript file calendar.js was provided for the assignment
* In order for the current date to be calculated properly, I had to invoke selDateArray = selDate.split("/") command