# agent5.5
index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Agent 5.5 is calling...</title>
  <link rel="stylesheet" href="agent55-call.css" /> <!-- Link to CSS style -->
  <style>
    /* (Optional) Inline CSS if not using external CSS file */
  </style>
</head>
<body>

<div class="call-screen">
  <!-- Caller information -->
  <!-- Optional caller image/avatar for Agent 5.5 -->
  <!-- <img src="agent55_avatar.png" alt="Agent 5.5" class="caller-photo"> -->
  <div class="caller-name">Agent 5.5</div>
  <div class="call-status">Incoming Call...</div>
  
  <!-- Call control buttons -->
  <div class="button-row">
    <button id="declineBtn" class="call-btn decline">Decline</button>
    <button id="answerBtn" class="call-btn answer">Answer</button>
  </div>
</div>

<!-- Hidden audio element with Agent 5.5's voice message -->
<audio id="agentVoice" src="agent55_johnpork_message.mp3" preload="auto"></audio>

<script src="agent55-call.js"></script> <!-- Link to JS functionality -->
<script>
  // (Optional) Inline JS if not using external file
</script>
</body>
</html>
style.css
/* Full-screen call screen container */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  background: #000; /* fallback background */
}
.call-screen {
  display: flex;
  flex-direction: column;
  justify-content: center;    /* center content vertically */
  align-items: center;        /* center content horizontally */
  height: 100vh;
  width: 100%;
  background: radial-gradient(circle, rgba(0,0,0,0.8) 20%, #000 100%); 
  /* ^ Example: a dark radial gradient for background (looks like a dimmed screen) */
  text-align: center;
  color: #f0f0f0; /* light text for contrast against dark background */
  font-family: sans-serif;    /* you can use a specific font from your site here */
  position: relative;
}

/* (Optional) Caller photo/avatar */
.caller-photo {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1rem;
  /* Add a border or shadow if desired to make it stand out */
}

/* Caller name and status text */
.caller-name {
  font-size: 1.8rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}
.call-status {
  font-size: 1.2rem;
  opacity: 0.8;
  margin-bottom: 2rem;
  /* Perhaps a blinking animation could be added to "Incoming Call..." for effect */
}

/* Button row container */
.button-row {
  display: flex;
  gap: 2rem;            /* space between the two buttons */
  margin-top: auto;     /* push buttons towards bottom of screen */
  margin-bottom: 3rem;  /* add some bottom margin for spacing */
}

/* Base style for call buttons */
.call-btn {
  font: 1rem sans-serif;
  font-weight: bold;
  padding: 0.8rem 1.4rem;
  border: none;
  border-radius: 999px;    /* very round corners (pill shape) */
  color: #fff;
  cursor: pointer;
  min-width: 100px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.3);
  transition: transform 0.1s ease;
}
.call-btn:active {
  transform: scale(0.97);   /* slight press effect on click */
}

/* Specific styles for Answer and Decline buttons */
.call-btn.answer {
  background-color: #4caf50;   /* green */
}
.call-btn.decline {
  background-color: #e53e3e;   /* red */
}

/* (Optional) Button hover effects */
.call-btn:hover {
  opacity: 0.9;
}

/* (Optional) If you want circular icon-style buttons (alternative to pill shape) */
/*
.call-btn {
  width: 80px; height: 80px;
  border-radius: 50%;
  padding: 0;
  font-size: 0.9rem;
}
.call-btn.answer::before,
.call-btn.decline::before {
  content: "📞";  // placeholder emoji or icon before text
  display: block;
  font-size: 1.5rem;
}
.call-btn.decline::before { content: "✖️"; }
*/
// Select elements by their IDs
const answerBtn = document.getElementById('answerBtn');
const declineBtn = document.getElementById('declineBtn');
const agentVoice = document.getElementById('agentVoice');
const callStatus = document.querySelector('.call-status');

// Click handler for Answer
answerBtn.addEventListener('click', () => {
  // Play the Agent 5.5 voice message
  agentVoice.play().catch(err => {
    console.error("Audio play failed:", err);
  });
  
  // Update UI to show call is answered (optional enhancements)
  if (callStatus) {
    callStatus.textContent = "Call Connected...";  // change status text
  }
  answerBtn.style.display = 'none';   // hide Answer button once answered
  declineBtn.textContent = 'End Call';// you could change Decline to 'End Call'
  // (Optionally, you could start a timer or other visuals here)
});

// Click handler for Decline/End Call
declineBtn.addEventListener('click', () => {
  // If the call was answered and audio is playing, stop the audio
  if (!answerBtn.style.display || answerBtn.style.display !== 'none') {
    // Call was not answered yet (user declined immediately)
    // You might play a quick beep or just do nothing special.
  } else {
    // Call was answered and now user clicks "End Call"
    agentVoice.pause();
    agentVoice.currentTime = 0; // reset audio to start if needed
  }
  // Redirect back to main page
  window.location.href = "index.html"; 
  // ^ Change "index.html" to your actual main page filename or URL as needed.
});
agentVoice.onended = () => {
  callStatus.textContent = "Call Ended";
  setTimeout(() => window.location.href = "index.html", 2000);
};
