---
layout: default
title: "Assorted 3d work"
categories: [3D, graphic design]
---
<div id="mainContent" class="gridContent">
	<div id="game-idea-container">
		<h1 id="game-idea-title">Song challenge:</h1>
		<p>
			Make a(n)
			<span id="song-energy" class="song-info active">energy</span>
			<span id="song-vibe" class="song-info active">vibe</span>
			<span id="song-genre" class="song-info">genre</span>
			song
			<span id="song-key" class="song-info">key</span>
			<span id="song-bpm" class="song-info">bpm</span>
			<span id="song-signature" class="song-info">signature</span>
			<span id="song-topic" class="song-info active">topic</span>
			<span id="song-instrument" class="song-info active">instrument</span>
		</p>
		<p>extra challenge: <span class="song-info">awd232ed</span></p>
		<button id="settings-button">Settings</button>
		<button id="generate-button">Generate</button>
		<div id="game-settings">
			<span id="settings-menu-title">Display or hide variables:</span>
			<label class="switch"><input type="checkbox" id="nrg-toggle" checked><span class="slider">Energy</span></label>
			<label class="switch"><input type="checkbox" id="vibe-toggle" checked><span class="slider">Vibe</span></label>
			<label class="switch"><input type="checkbox" id="genre-toggle"><span class="slider">Genre</span></label>
			<label class="switch"><input type="checkbox" id="key-toggle"><span class="slider">Key</span></label>
			<label class="switch"><input type="checkbox" id="bpm-toggle"><span class="slider">BPM</span></label>
			<label class="switch"><input type="checkbox" id="signature-toggle"><span class="slider">Signature</span></label>
			<label class="switch"><input type="checkbox" id="topic-toggle" checked><span class="slider">Topic</span></label>
			<label class="switch"><input type="checkbox" id="instrument-toggle" checked><span class="slider">instrument</span></label>
		</div>
	</div>
</div>
<script>
	// Store all categories in a single object
const songData = {
  vibes: [
    "melodic", "haunting", "uplifting", "soulful", "dreamy", "intense", "bittersweet", "ethereal", 
    "gritty", "electrifying", "soothing", "hypnotic", "raw", "nostalgic", "explosive", "groovy", 
    "serene", "powerful", "euphoric", "catchy", "mournful", "majestic", "romantic", "dark", "playful", 
    "moody", "thrilling", "jazzy", "epic", "cinematic", "whimsical", "passionate", "chill", "dynamic", 
    "dramatic", "warm", "grungy", "funky", "energetic", "ambient", "mellow", "poignant", "spiritual", 
    "rhythmic", "spacy", "edgy", "trippy", "vibrant", "introspective", "minimalist", "aggressive", "anthemic"
  ],
  energyLevel: [
  	"super low energy", "low energy", "medium energy", "high energy", "super high energy"
  ],  
  genres: [
    "Action", "Adventure", "Simulation", "Strategy", "Role-Playing"
  ],
  basicGenres: [
    "pop", "hip-Hop", "rock", "country", "EDM", "classical", "folk"
  ],
  topics: [
    "the joy of finding love", "the pain of a breakup", "a place", "the story of your life", "wanting freedom", 
    "being deceived", "hopes and dreams", "being hurt", "disappointment", "going somewhere (metaphorical or literal)", 
    "being watched / watching someone", "food", "religion", "anxiety", "partying", "a dance move", "happiness", 
    "flying", "home", "saying goodbye", "having fun", "the hustle", "music", "heroes", "money", "driving", "robots", 
    "a different world", "violence", "goals"
  ],
  keys: [
  	"C", "C♯", "D", "D♯", "E", "F", "F♯", "G", "G♯", "A", "A♯", "B", "Cm", "C♯m", "Dm", "D♯m", "Em", "Fm", "F♯m", "Gm", "G♯m", "Am", "A♯m", "Bm"
  ],
  signatures: [
  	"4/4", "3/4", "2/4", "6/8", "9/8", "12/8", "5/4", "7/8", "11/8", "15/8", "5/8", "13/8", "3/8"
  ],
  instruments: [
  	"piano", "guitar", "bass", "drums", "violin", "cello", "trumpet", "saxophone", "flute", "clarinet", "trombone", "harp", "synthesizer", "accordion", "ukulele", "samples", "acapella", "instrument you don't usually use"
  ]

};

// Store UI elements in an object for easy access
const uiElements = {
  energy: document.querySelector("#song-energy"),
  vibe: document.querySelector("#song-vibe"),
  genre: document.querySelector("#song-genre"),
  key: document.querySelector("#song-key"),
  bpm: document.querySelector("#song-bpm"),
  signature: document.querySelector("#song-signature"),
  topic: document.querySelector("#song-topic"),
  instrument: document.querySelector("#song-instrument"),
  generateButton: document.querySelector("#generate-button"),
  settingsButton: document.querySelector("#settings-button"),
  settingsMenu: document.querySelector("#game-settings"),
};

console.log(uiElements);

// Function to get a random item from any category
const getRandomItem = (category) => {
  const items = songData[category]; // Access the correct array from songData
  return items[Math.floor(Math.random() * items.length)];
};

// Event listener for generating a song idea
uiElements.generateButton.addEventListener("click", () => {

	const includeEnergy = document.getElementById("nrg-toggle").checked;
    const includeVibe = document.getElementById("vibe-toggle").checked;
    const includeGenre = document.getElementById("genre-toggle").checked;
    const includeKey = document.getElementById("key-toggle").checked;
    const includeBPM = document.getElementById("bpm-toggle").checked;
	const includeSignature = document.getElementById("signature-toggle").checked;
    const includeTopic = document.getElementById("topic-toggle").checked;
    const includeInstrument = document.getElementById("instrument-toggle").checked;

    includeEnergy ? (uiElements.energy.classList.add("active")) : uiElements.energy.classList.remove("active") ;
    includeVibe ? (uiElements.vibe.classList.add("active")) : uiElements.vibe.classList.remove("active") ;
    includeGenre ? (uiElements.genre.classList.add("active")) : uiElements.genre.classList.remove("active") ;
    includeKey ? (uiElements.key.classList.add("active")) : uiElements.key.classList.remove("active") ;
    includeBPM ? (uiElements.bpm.classList.add("active")) : uiElements.bpm.classList.remove("active") ;
    includeSignature ? (uiElements.signature.classList.add("active")) : uiElements.signature.classList.remove("active") ;
    includeTopic ? (uiElements.topic.classList.add("active")) : uiElements.topic.classList.remove("active") ;
    includeInstrument ? (uiElements.instrument.classList.add("active")) : uiElements.instrument.classList.remove("active") ;

  uiElements.energy.textContent = getRandomItem("energyLevel");
  uiElements.vibe.textContent = getRandomItem("vibes");
  uiElements.genre.textContent = getRandomItem("basicGenres"); // Adjust if using "genres"
  uiElements.key.textContent = "in " + getRandomItem("keys");
  uiElements.bpm.textContent = "at ±" + (Math.floor(Math.random() * (250 - 40 + 1)) + 40) + " BPM";
  uiElements.signature.textContent = "in " + getRandomItem("signatures");
  uiElements.topic.textContent = "about " +getRandomItem("topics");
  uiElements.instrument.textContent = "using a(n) " +getRandomItem("instruments");

});

// Event listener for settings
uiElements.settingsButton.addEventListener("click", () => {
	uiElements.settingsMenu.classList.toggle("active");
});


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
	color: #454545;
    border: 1.5px solid #454545;
    border-radius: 30px;
    padding: 3px 10px;
    cursor: crosshair;
}

.song-info:hover{
	color: white;
	background-color: #2965ff;
	border-color: #2965ff;
}

.song-info.active{
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
	.song-info.active{
		white-space: nowrap;
	}
	#settings-menu-title{
		width: 100%;
	}
    #game-settings {
        display: flex;
        flex-wrap: wrap;
        row-gap: 8px;
        column-gap: 2px;
    }
}
}
</style>