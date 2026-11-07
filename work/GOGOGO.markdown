---
layout: work
title:  "GOGOGO! - Job interview project"
categories: [Font design]
---

<div id="column1_6">
	<p><img src="/media/images/gogogo/Desktop - 4.png" class="zoom"></p>
	<p><img src="/media/images/gogogo/Desktop - 1.png" class="zoom"></p>
	<p><img src="/media/images/gogogo/match.png" class="zoom"></p>
</div>

<div id="column6_13">
	<span id="projectCats">{{ page.categories | join: " / " }}</span>
	<h1>{{page.title}}</h1>
	<p>GOGOGO is a 13x13 online game of go I made as a part of a job application.</p>
	<h2>The assignment</h2>
	<p>Design and implement Go game</p>
		<ul>
			<li>Board size: 13x13</li>
			<li>The first two players can start the game.</li>
			<li>After the game has started, others can watch it.</li>
			<li>The first two players can chat with each other during the game.</li>
</ul>
<h2>Deliverables:</h2>

	<ul>
	<li>Link to the source code (either GitHub or GitLab)</li>
	<li>The source code must contain a docker-compose file to run two containers (os: Linux)
</li>
		<ul class="indentListItem">
			<li>The webserver</li>
			<li>The database (should be PostgreSQL)</li>
		</ul>
	<li>The source code must contain a report (.pdf) explaining the design and implementation.
</li>
	</ul>
<p>
Based on your skill set and time:
</p>
		<ul>
			<li>In addition to the frontend, you can decide what to focus on in this project (user experience, backend, game engine, or ...). Please note that the evaluation will be based solely on your resume. There's no need to worry if you don't have a particular skill set.
</li>
			<li>You can choose your preferred technology stack.</li>
			<li>You are allowed and encouraged to use AI, except <a href="https://en.wikipedia.org/wiki/Vibe_coding">vibecoding</a> (remember to explicitly mention any use of AI in the report: LLMs, Copilot, APIs, ...)</li>
</ul>
	<h2>Research</h2>
	<p>Before I even started writing anything, the first thing I did was to look up the game. I had never heard of it before and as such had to familiarize myself with it and its rules. This was done by simply watching a youtube series for beginners.</p>
	<p>Once I felt I had some basic understanding of the game, my next step involved looking up other implementations of the game that I could test out, especially open source ones also written in javascript. I found a few excellent examples, the main ones being <a href="https://github.com/waltheri/wgo.js">WGo.js</a> as well as <a href="https://github.com/aprescott/tenuki">tenuki</a> which I referenced quite often throughout development. I considered using their code directly as they should be easy to slot in, and depending on the time it would take to implement the entire game from scratch I would decide if I was going to do it from scratch or use some already existing implementation. Ultimately, due to a time constraint as well as my very shallow understanding of the game, I decided to use a premade solution that I then tweaked to better fit my use.</p>
	<p>I followed this by asking GPT how it would go about doing the project in broad strokes, hoping to get some guidance without necessarily going too in depth. What GPT recommended was using React in the frontend with Express and NodeJS in the backend. This should go very well with PostgreSQL and has the benefit (for me atleast) of using most of the elements of the MERN stack (which is my goto). </p>
	<p>My next step was researching examples of games with websocket solutions, taking primarily inspiration from a game like Jackbox games that use Socket.io. This is because websocket is extremely suitable for games where you need live interaction, additionally the two players should be able to chat, making websocket a no-brainer solution due to its fast responses.</p>
	<h2>Pre-planning</h2>
	<p>Once I had figured out a basic idea of what I wanted to do, I started working on a small figma project to figure out how i wanted the layout to be and the look of the project: This in itself is not necessarily the most important step when you’re on a time crunch and still trying to figure out how things will work, however a good GUI is an important part of the end product, and I wanted to make sure it looks polished.</p>
	<p>I did some brainstorming regarding what I wanted to do aesthetically and since we were not given any directions on style, and there was no specific market this project would cater to, I took the liberty of just making something that I personally would enjoy. My main inspiration then came from my usual pool of slightly futuristic, sleek UIs primarily inspired by video games. Given the time crunch (and the fact I did not know how long it would actually take to implement the core functionality) I chose to not go all out on this, while still keeping the general vibe I was going for.</p>
	<p>OOne of my goals for this was to hopefully stand out by not doing the same skeuomorphic UI most implementations of the game use and my goal for the design was to look like something you’d see in a cool cyber cafe in 2050.</p>
	<p>I also decided that one of the things I would do for this project is try out tailwind. I have wanted to try a CSS framework for a long time since I usually write my CSS myself and this is the first project I’ve done in a while where I could test it out.</p>
	<h2>Development</h2>
	<h3>Frontend</h3>
	<p>After determining which technologies would be suitable for the project I began implementing the frontend by setting up the core UI components in react and tailwindCSS. I had not yet decided exactly how I would implement the game board, but I had a general idea of how I wanted the layout to be which was enough to start. I hardcoded the components I knew would be necessary as a start. This is what I usually do for react projects as it allows me to test things, and then later I add the functionality needed.</p>
	<p>After the backend was up and running I connected the chat component to the socket system, and added rooms so that chats sent in one room are only shared with that room. Here I realized I’d need a way to show not only the room code, but also game information such as a score (represented by amount of captures). I then altered the UI somewhat to support this.</p>
	<h3>Backend</h3>
	<p>Once I had a good start on the front-end I started introducing elements of the backend, by just setting up basic express and cors things I needed before doing anything else. After this was done I set up the docker containers and docker compose file so that everything can easily be deployed by the interviewer later on. </p>
	<p>I then started setting up the socket.io connections which was a bit tricky at first as I had never used it before, and only had minimal experience with websockets in general. I started testing some of the functions of websockets, before connecting it up to the react frontend using the socket.io client, and once I was comfortable with this I started actually connecting this up to the postgres database from docker.</p>
	<p>I also figured that since the game needs to be created before anything else happens, I used a standard REST API method to create a user and game, and then immediately join the game as the first user, ensuring that no one else can hijack the room. And only after this does the game start using the socket connection.</p>
</div>