---
layout: project
title:  "Music idea generator"
categories: [Web, In progress]
---


<div id="column1_13">
	<span id="projectCats">{{ page.categories | join: " / " }}</span>
	<h1>{{page.title}}</h1>
	<span id="notif">PS: This is a living document, more information about the project will come as I keep working on it.</span>
	<h2>Introduction</h2>
	<p>Some of you might know this about me but I also like to make music as a hobby once in a while. This and the fact that I have musician friends, pushed me to make a little tool for generating music challenges for when you're really stuck. The point of making it a challenge is that you have to push yourself to do something different, while not having the pressure of making something you need to share with others. In my opinion this tends to make loosen up somewhat and play with ideas I normally wouldn't such as trying different genres or instrumnents I dont usually do.</p>
	<h2>The Idea</h2>
	<p>I knew I wanted to create something simple that is somewhat customizable, and I knew I wanted to make it fit with my visual style. That was my main ideas and then stuff like extra challenges and being able to lock options came later.</p>
	<h2>Development</h2>
	<p>During development I realized that I was going to need to change the sentence structure to make it grammatically correct. This actually took some testing on my part as the english grammar rules weren't always so obvious. In the first version of the generator i would structure sentences like this:
	<code>Make a(n) super low energy rhythmic song about the hustle using a(n) bass</code>
	<br/>
	As I had simply hardcoded the indefinite article as a(n) for all options as I wasn't sure how I was going to accurately select it.
	</p>
	<p>In the end I opted to use a json file with the article as well as the affixes. This proved to be the simplest way to do it for me as it gave me a lot of flexibility without having to code parsing for each exception. As an example, a json object might look like this for a key<code>{ "value": "the joy of finding love", "prefix": "about" }</code>
	And then I can simply use a generic renderer for all of the options.
	</p>
	<p>I also talked to some of my friends to get feedback and suggestions on the app which is where I got the idea to be able to lock options and also the option to finely tweak settings (I haven't implemented that yet but there will be finer options for stuff like genre specificity etc.</p>
	<h2>Try it now</h2>
	<p>Version 2 of the music generator <a href="/music-idea-generator">should now be live</a>. Feel free to test it and give me any feedback/ideas/wishes &lt;3 </p>
</div>

