---
layout: default
title: "Assorted 3d work"
categories: [3D, graphic design]
---
<div id="mainContent" class="gridContent">
	<div id="game-idea-container">
		<h1 id="game-idea-title">Song challenge:</h1>
		<p style="line-height: 2;">
			Make <span id="song-article">a</span>
			<span id="song-energy" class="song-info first active"> <span class="song-info-value">energy</span></span>
			<span id="song-vibe" class="song-info first active"><span class="song-info-value">vibe</span>
			</span>
			<span id="song-genre" class="song-info first active"><span class="song-info-value">genre</span></span>
			song
			<span id="song-key" class="song-info first active">in <span class="song-info-value">key</span></span>
			<span id="song-bpm" class="song-info first active">at <span class="song-info-value">±BPM</span></span>
			<span id="song-signature" class="song-info first active">in <span class="song-info-value">time signature</span></span>
			<span id="song-topic" class="song-info first active">about <span class="song-info-value">topic</span></span>
			<span id="song-instrument" class="song-info first active">with <span class="song-info-value">instrument</span></span>
			<span id="song-extra_challenge" class="song-info first active">with <span class="song-info-value">extra challenge</span></span>
		</p>
		<button id="settings-button">Settings</button>
		<button id="generate-button">Generate</button>
		<div id="game-settings">
			<span id="settings-menu-title">Display or hide variables:</span>
			<label class="switch"><input type="checkbox" id="energy-toggle"><span class="slider">Energy</span></label>
			<label class="switch"><input type="checkbox" id="vibe-toggle"><span class="slider">Vibe</span></label>
			<label class="switch"><input type="checkbox" id="genre-toggle"><span class="slider">Genre</span></label>
			<label class="switch"><input type="checkbox" id="key-toggle"><span class="slider">Key</span></label>
			<label class="switch"><input type="checkbox" id="bpm-toggle"><span class="slider">BPM</span></label>
			<label class="switch"><input type="checkbox" id="signature-toggle"><span class="slider">Signature</span></label>
			<label class="switch"><input type="checkbox" id="topic-toggle"><span class="slider">Topic</span></label>
			<label class="switch"><input type="checkbox" id="instrument-toggle"><span class="slider">instrument</span></label>
			<label class="switch"><input type="checkbox" id="extra_challenge-toggle"><span class="slider">extra</span></label>
		</div>
	</div>
</div>
<script>
	const uiElements = {
	  energy: document.querySelector("#song-energy"),
	  vibe: document.querySelector("#song-vibe"),
	  genre: document.querySelector("#song-genre"),
	  key: document.querySelector("#song-key"),
	  bpm: document.querySelector("#song-bpm"),
	  signature: document.querySelector("#song-signature"),
	  topic: document.querySelector("#song-topic"),
	  instrument: document.querySelector("#song-instrument"),
	  extra_challenge: document.querySelector("#song-extra_challenge"),
	  generateButton: document.querySelector("#generate-button"),
	  settingsButton: document.querySelector("#settings-button"),
	  settingsMenu: document.querySelector("#game-settings"),
	};

	let isFirstTime = true;

	// Store all categories in a single object
	let options = {};
	const selected = {};
	
	const active = {
	    energy: true,
	    vibe: true,
	    genre: false,
	    key: false,
	    bpm: false,
	    signature: false,
	    topic: true,
	    instrument: true,
	    extra_challenge: true
	};
	
	let locked = {
	    energy: false,
	    vibe: false,
	    genre: false,
	    key: false,
	    bpm: false,
	    signature: false,
	    topic: false,
	    instrument: false,
	    extra_challenge: false,
	};
	
	fetch('./options.json')
	.then(response => response.json())
	.then(data => {
	    options = data;      // Nå er 'options' fylt med JSON-objektet ditt!
	})
	.catch(error => console.error("Feil under lasting av JSON:", error));

	//generates new song ideas when clicking on generate
	uiElements.generateButton.addEventListener("click", () => generateSong());

	//toggles the settings menu when clicking on settings
	uiElements.settingsButton.addEventListener("click", () => { uiElements.settingsMenu.classList.toggle("active"); });

	function setInitial(){
		console.log("this should only run ONCE!!");

		// makes the active buttons show as active under settings
		Object.keys(active).forEach(key => {
			document.getElementById(`${key}-toggle`).checked = active[key];
		});

		// makes sure the default active keys are shown and hides the other ones using "first" class.
		Object.keys(active).forEach(key => {
			if(!active[key]){
				document.getElementById(`song-${key}`).classList.remove("active");
			}
			
		});
	}

	setInitial();

	Object.keys(locked).forEach(key => {
		uiElements[key].addEventListener("click", (event) => {
			if (uiElements[key].classList.contains("first")) {
				return;
			}

			locked[key] = !locked[key];
			uiElements[key].querySelector('.song-info-value').classList.toggle("locked", locked[key]);
		})
	})


	Object.keys(active).forEach(key => {
	  document.getElementById(`${key}-toggle`).addEventListener("change", (event) => {
	      active[key] = event.target.checked;

	      const element = document.getElementById(`song-${key}`);
	      element.classList.toggle("active", active[key]);
	      if (isFirstTime) {element.classList.add("first");}
	      
	  });
	});
	

	function generateSong() {
		isFirstTime = false;
		Object.keys(active).forEach(key => {
			document.getElementById(`song-${key}`).classList.remove("first");
		});

	    // Randomly select an option for every tag
	    Object.keys(options).forEach(tag => {
	        const list = options[tag];

	        if(locked[tag]){
	        	console.log(`locked item ${tag}`);
	        	return;
	        }

	        if(tag == "genre"){
	        		if(locked.genre) {
	        			selected.genre = selected.genre || {"value": "3"};
	        			return;
	        		};
	        		const genrelist = options.genre.basic;
	        		selected.genre = genrelist[Math.floor(Math.random() * genrelist.length)];
	        		return;
	        }

	        if(tag == "bpm"){
	        	selected.bpm = {"value": (Math.floor(Math.random() * (250 - 40 + 1)) + 40).toString(), "suffix": "BPM", "prefix": "at" };
	        	console.log({selected});
	        	return;
	        }

	        selected[tag] = list[Math.floor(Math.random() * list.length)];
	    });

	    renderSong();
	}
		
		
		function renderSong() {
		
		    const tags = Object.keys(options);
		
		    // Find the first active tag
		    const firstActive = tags.find(tag => active[tag]);
		
		    // Set opening a/an
		    const article = firstActive
		        ? selected[firstActive].article ||
		          (/^[aeiou]/i.test(selected[firstActive].value.trim()) ? "an" : "a")
		        : "a";
		
		    document.getElementById("song-article").textContent = article;
		
		    // Render each tag in its fixed position
		    tags.forEach(tag => {
		
		        const element = document.getElementById(`song-${tag}`);
		        const option = selected[tag];
		
		        element.classList.toggle("active", active[tag]);
		
		        // Clear previous content
		        element.replaceChildren();
		
		        // Prefix
		        if (option?.prefix) {
		            element.append(document.createTextNode(option.prefix + " "));
		        }
		
		        // Article
		        if (option?.article) {
		            element.append(document.createTextNode(option.article + " "));
		        }
		
		        // Highlighted value
		        const value = document.createElement("span");
		        value.textContent = option.value;
						value.classList.add("song-info-value");
						value.classList.toggle("locked", locked[tag]);
		        element.append(value);
		
		        // Suffix
		        if (option.suffix) {
		            element.append(document.createTextNode(" " + option.suffix));
		        }
		    });
		}
</script>

<style type="text/css">
	#game-idea-container {
		grid-column: 1/ span 12;
	}

	#game-idea-title {
		font-size: 32px;
		margin-bottom: 20px;
	}

	button {
		background-color: white;
		color: #454545;
		border-radius: 10em;
		font-size: 17px;
		font-weight: 600;
		padding: 0.8em 1.6em;
		cursor: pointer;
		transition: box-shadow 0.2s ease-in-out, transform 0.2s ease-in-out;
		border: 1.5px solid #454545;
		box-shadow: 0 0 0 0 #454545;
		user-select: none;
	}

	button:hover {
		transform: translateY(-4px) translateX(-2px);
		box-shadow: 2px 5px 0 0 #454545;
	}

	button:active {
		color: white;
		background-color: #2965ff;
	}

	.song-info {
	    display: none;
	}

	.song-info.active,
	.song-info.active .song-info-value {
	    display: inline;
	    white-space: nowrap;
	}
	.song-info.first .song-info-value{
		display: inline;
    color: #454545;
    border: 1.5px solid #454545;
    border-radius: 30px;
    padding: 3px 10px;
    cursor: pointer;
	}

	.song-info.first .song-info-value:hover{
    color: white;
    border-color: #2965ff;
	}

	.song-info.first .song-info-value:after, .song-info.first .song-info-value:before{
		content: unset;
	}

	.song-info-value {
		display: none;
		color: #454545;
	    border: 1.5px solid #454545;
	    border-radius: 30px;
	    padding: 3px 10px;
	    cursor: pointer;
	}

	.song-info-value:after {
		content: "🔓";
		font-variant-emoji: text;
		font-size: 17px;
		margin-left: 3px;
	}

	.song-info-value.locked:after {
		color: #2965ff;
	}

	.song-info-value:hover:after, .song-info-value.locked:after {
		content: "🔒";
		font-variant-emoji: text;
		font-size: 17px;
		margin-left: 3px;
		color: #2965ff;
	}

	.song-info-value:hover:after{
		color: white;
	}

	.song-info-value.locked:hover:after{
		content: "🔓";
	}

	.song-info-value:hover{
		color: white;
		background-color: #2965ff;
		border-color: #2965ff;
	}

	.song-info.active, .song-info.active .song-info-value{
		display: inline;
	}

	.switch input {
		opacity: 0;
		width: 0;
		height: 0;
	}

	.slider {
		background-color: white;
		color: #454545;
		border-radius: 10em;
		font-size: 17px;
		font-weight: 600;
		padding: 0.8em 1.6em;
		cursor: pointer;
		-webkit-transition: .2s;
		transition: .2s;
		font-family: 'Roboto', sans-serif;
		border:1.5px solid #454545;
		display: inline-block;
		user-select: none;
	}

	input:checked+.slider {
		background-color: #2965ff;
		color: white;
		border-color: white;
	}

	#game-settings{
		padding: 40px 0;
		display: none;
	}

	#game-settings.active{
		display: block;
	}

	#settings-menu-title{
		font-size: 32px;
		font-weight: 500;
		margin-bottom: 20px;
		display: block;
	}

	@media only screen and (max-width: 850px) {
		#game-idea-container p {
			line-height: 42px;
		}
		.song-info-value.active{
			white-space: nowrap;
		}
		#settings-menu-title{
			width: 100%;
		}
	    #game-settings {
	        flex-wrap: wrap;
	        row-gap: 8px;
	        column-gap: 2px;
	    }
	    #game-settings.active{

	    }
	}
	}
</style>
