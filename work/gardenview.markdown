---
layout: work
title:  "Gardenview"
categories: [Front-end, visual identity, logo]
---

<div id="column1_6">
	<p><img src="/media/images/gardenview_1.png" class="zoom"></p>	
	<p><img src="/media/images/gardenview_2.png" class="zoom"></p>
</div>

<div id="column6_13">
	<span id="projectCats">{{ page.categories | join: " / " }}</span>
	<h1>{{page.title}}</h1>
	<p>
		The gardenview project was a project developed while studying at <acronym title="Norges teknisk-naturvitenskapelige universitet">NTNU</acronym> which aims to create a fully usable website for taking care of your plants. Specifically the use case for this would be an office building or any similar structures where multiple people are to take care of many plants.
	</p>	
	<p>
		The website was a project between myself and 3 other students and each of us had our own main parts in the development. For me the main focus was design and front-end development. The bounds for the project were outlined by our professor and beyond that we had free reign to do as we wanted. As such we had a design and prototyping phase where we did a few iterations of design and then contacted the project owner for approval on our design.
	</p>
	<p>
		After this we started working on the backend and creating an API thats suitable for the project as well as setting up the database. One of the requirements for the project was setting up different roles with different permissions that would only be accessible to those with the right role. those not logged in are able to see all the plants but not interact, while gardeners are also allowed to water plants. The manager role is allowed to do both of these, as well as being able to manage gardeners.
	</p>
	<p><a href="https://gardenview.netlify.app/" target="_blank">Check out the webiste here</a></p>
</div>