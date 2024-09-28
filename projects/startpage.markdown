---
layout: project
title:  "New Startpage"
categories: [Web, not started]
---

<div id="column1_13">
	<span id="projectCats">{{ page.categories | join: " / " }}</span>
	<h1>{{page.title}}</h1>
	<span id="notif">PS: This is a living document, more information about the project will come as I keep working on it.</span>
	<p>In my 3 years as a student at NTNU I’ve designed and made multiple startpages for my browser. A startpage is an HTML file that appears when you open a new tab, and serves as a hub for easy access to your most used websites and other information. Common elements of a startpage would be information such as links, a clock, and some sort of decorative element. In terms of design and coding they are usually not very complex, but simple utilitarian projects that also provide an aesthetic quality for its user (which in this case is me).</p>
	<p>Below is an example of the most recent design I created. This design, while visually appealing and functional for the time I used it, has some issues regarding readability, flexibility for different screensizes and being dependent on external widgets (the weather module is not made by me). Additionally I would like a new fresh design, that prioritizes the information I want, and with a new look, that fits my current aesthetic preferences.</p>
	<p><img src="/media/images/startpage_project.png" class="zoom" alt="startpage userinterface on a modern building facade background image"></p>
	<p>Given this, I wish to make a new one, with a more minimal, less cramped look, that also incorporates my own weather widget using the <a href="https://developer.yr.no/doc/locationforecast/HowTO/" target="_blank">API from Yr</a>. I'm thinking I might drop the news feed and possibly create a tabs system, as well as a simpler weather widget, possibly something inspired by smart mirrors or scifi movie UIs.</p>
</div>


