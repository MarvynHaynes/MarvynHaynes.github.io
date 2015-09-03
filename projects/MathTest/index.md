---
layout:     page
title:      Math Test
date:       2013-03-04 10:03:26
summary:    A simple game of math questions created in C# & WPF created for a school project.
categories: Project
author:     Marvyn
thumbnail:  briefcase
addCSS:     myCustom.css
tags:
 - C#
 - Project
---

<img class="thumbnail" src="{{ site.baseurl }}/projects/MathTest/images/MathTest.jpg" alt="Math Test Screenshot">

# Summary

A simple C# GUI program that will test users on 10 addition and subtraction questions.  

### Interface

The simple interface was created using WPF that uses StackPanel elements with Grid.Row attributes for the layout of each section to provide a simple and clean look.  The top panel is used for the main menu items, with the following panels reserved for the question number, the math question textbox, answer textbox and check answer button, and the bottom panel reserved for the next question button.


### Menu System Layout & Functions

The layout and functions of the menu system I created using WPF are similarly found in most windows apps:


<table border="0" cellpadding="1" cellspacing="1" style="width: 500px;">
	<tbody>
		<tr>
			<td><strong>_File</strong></td>
			<td><strong>_Edit</strong></td>
			<td><strong>_Tools</strong></td>
			<td><strong>_Help</strong></td>
		</tr>
		<tr>
			<td>_New Test</td>
			<td>_Copy</td>
			<td>_See Report</td>
			<td>_About</td>
		</tr>
		<tr>
			<td>_Exit</td>
			<td> </td>
			<td> </td>
			<td> </td>
		</tr>
	</tbody>
</table>


*Note: _ denotes the hotkey letter when user presses the key.  ex: _File is alt-f, _Edit is alt-e, _Copy is alt-c etc. etc.*

* New Test - resets variables and starts a new test
* Copy - allows the user to copy selected text from the text box
* See Report - opens the ReportWindow
* About - opens a message box with the authors' name
* Exit - closes down the program
 

### Gamplay Logic

The program is best described in 4 states:

 1. **Starting State**: Just started, or after New Test menu was used Note: Message Boxes are used to notify the user of bad inputs and they remain in this state until a ‘good’ input is received.
 2. **Check Answer Used State**: User has typed into the answer text box and just clicked the Check Answer Button.
 3. **Next Question Used State**: Next Question button was just clicked and Question 1 becomes Question 2.
 4. **End of Test State**: The user checked their 10th answer, and then clicked Next Question. A Message Box notifies them the test was over and both buttons (_Check Answer and Next Question_) are now disabled. They need to use the menu to start a new game.
 

### The Report Window

<img src="{{ site.baseurl }}/projects/MathTest/images/ReportWindow.jpg" alt="Report Window Screenshot">

When the user clicks on Tools and See Report, a new window is shown and simply displays the questions and answers. The text making up the report was placed within a Textbox, which is within a Scroll Viewer.