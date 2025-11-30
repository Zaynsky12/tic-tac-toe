<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover">
<title>Tic Tac Toe - Futuristic Battle Arena</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800&display=swap" rel="stylesheet">
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  background: #0a0e27;
}

body {
  font-family: 'Orbitron', monospace, sans-serif;
  background: linear-gradient(135deg, #0a0e27 0%, #1a0b2e 50%, #16003b 100%);
  background-attachment: fixed;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  overflow-x: hidden;
  overflow-y: auto;
  touch-action: pan-y;
  -webkit-tap-highlight-color: transparent;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  user-select: none;
}

body::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-image: 
    repeating-linear-gradient(0deg, rgba(0, 255, 255, 0.05) 0px, transparent 1px, transparent 40px),
    repeating-linear-gradient(90deg, rgba(255, 0, 255, 0.05) 0px, transparent 1px, transparent 40px);
  pointer-events: none;
  animation: gridMove 20s linear infinite;
}

@keyframes gridMove {
  0% { transform: translate(0, 0); }
  100% { transform: translate(40px, 40px); }
}

.particle {
  position: absolute;
  width: 2px;
  height: 2px;
  background: #00ffff;
  border-radius: 50%;
  pointer-events: none;
  box-shadow: 0 0 5px #00ffff;
  animation: particleFloat 8s ease-in-out infinite;
  will-change: transform, opacity;
}

.particle:nth-child(2n) {
  background: #ff00ff;
  box-shadow: 0 0 5px #ff00ff;
  animation-duration: 10s;
  animation-delay: 2s;
}

@keyframes particleFloat {
  0% {
    transform: translate(0, 100vh) scale(0);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translate(100px, -100vh) scale(1);
    opacity: 0;
  }
}

body::after {
  content: '';
  position: absolute;
  width: 100%;
  height: 100%;
  background: radial-gradient(ellipse at center, rgba(0, 255, 255, 0.1) 0%, transparent 70%);
  pointer-events: none;
  animation: pulse 4s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 0.3; }
  50% { opacity: 0.6; }
}

@media (max-width: 600px) {
  body::after {
    display: none;
  }
}

#gameContainer {
  background: rgba(10, 14, 39, 0.85);
  border-radius: 20px;
  padding: 40px;
  box-shadow: 
    0 0 60px rgba(0, 255, 255, 0.3),
    0 0 100px rgba(255, 0, 255, 0.2),
    inset 0 0 40px rgba(0, 255, 255, 0.05);
  max-width: 600px;
  width: 100%;
  border: 2px solid rgba(0, 255, 255, 0.3);
  position: relative;
  z-index: 10;
  backdrop-filter: blur(10px);
  transform: translateZ(0);
  -webkit-transform: translateZ(0);
  margin: auto;
}

@media (max-width: 600px) {
  #gameContainer {
    backdrop-filter: none;
    box-shadow: 0 0 30px rgba(0, 255, 255, 0.2);
  }
}

#gameContainer::before {
  content: '';
  position: absolute;
  bottom: -30px;
  left: 50%;
  transform: translateX(-50%);
  width: 80%;
  height: 30px;
  background: radial-gradient(ellipse, rgba(0, 255, 255, 0.3) 0%, transparent 70%);
  filter: blur(15px);
  z-index: -1;
}

@media (max-width: 600px) {
  #gameContainer::before {
    display: none;
  }
}

h1 {
  text-align: center;
  color: #00ffff;
  margin-bottom: 10px;
  font-size: 2em;
  font-weight: 800;
  text-transform: uppercase;
  letter-spacing: 8px;
  text-shadow: 
    0 0 10px #00ffff,
    0 0 20px #00ffff;
  animation: titleColorShift 6s ease-in-out infinite;
}

@keyframes titleColorShift {
  0% { 
    color: #00ffff;
    text-shadow: 
      0 0 10px #00ffff,
      0 0 20px #00ffff,
      0 0 30px #00ffff,
      0 0 40px #00ffff;
  }
  33% { 
    color: #a855f7;
    text-shadow: 
      0 0 10px #a855f7,
      0 0 20px #a855f7,
      0 0 30px #a855f7,
      0 0 40px #a855f7;
  }
  66% { 
    color: #3b82f6;
    text-shadow: 
      0 0 10px #3b82f6,
      0 0 20px #3b82f6,
      0 0 30px #3b82f6,
      0 0 40px #3b82f6;
  }
  100% { 
    color: #00ffff;
    text-shadow: 
      0 0 10px #00ffff,
      0 0 20px #00ffff,
      0 0 30px #00ffff,
      0 0 40px #00ffff;
  }
}

.subtitle {
  text-align: center;
  color: #ff00ff;
  margin-bottom: 30px;
  font-size: 0.9em;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 0 0 10px #ff00ff;
}

#gameBoard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
  margin: 30px auto;
  max-width: 450px;
  padding: 20px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 15px;
  border: 1px solid rgba(0, 255, 255, 0.2);
  box-shadow: inset 0 0 30px rgba(0, 255, 255, 0.1);
}

.cell {
  aspect-ratio: 1;
  background: rgba(10, 14, 39, 0.6);
  border: 2px solid rgba(0, 255, 255, 0.4);
  border-radius: 10px;
  font-size: 4em;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 
    0 0 20px rgba(0, 255, 255, 0.3),
    inset 0 0 20px rgba(0, 255, 255, 0.05);
  position: relative;
  overflow: hidden;
  color: transparent;
  animation: cellIdlePulse 3s ease-in-out infinite;
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
  user-select: none;
  -webkit-user-select: none;
  will-change: transform;
  backface-visibility: hidden;
  -webkit-backface-visibility: hidden;
}

@keyframes cellIdlePulse {
  0%, 100% {
    border-color: rgba(0, 255, 255, 0.4);
  }
  50% {
    border-color: rgba(0, 255, 255, 0.6);
  }
}

.cell::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(45deg, transparent, rgba(0, 255, 255, 0.1), transparent);
  transform: translateX(-100%);
  transition: transform 0.6s;
}

.cell:hover:not(.taken)::before {
  transform: translateX(100%);
}

@media (max-width: 600px) {
  .cell::before {
    display: none;
  }
}

.cell:hover:not(.taken) {
  transform: scale(1.05);
  border-color: rgba(0, 255, 255, 0.9);
  box-shadow: 
    0 0 25px rgba(0, 255, 255, 0.5),
    inset 0 0 20px rgba(0, 255, 255, 0.2);
  background: rgba(0, 255, 255, 0.1);
  animation: none;
}

.cell.taken {
  cursor: not-allowed;
  animation: cellPlace 0.6s ease-out;
}

@keyframes cellPlace {
  0% { 
    transform: scale(0.3); 
    opacity: 0;
    filter: blur(10px);
  }
  50% { 
    transform: scale(1.3); 
    opacity: 0.8;
    filter: blur(2px);
  }
  100% { 
    transform: scale(1); 
    opacity: 1;
    filter: blur(0);
  }
}

.cell.x {
  color: #00ffff;
  background: rgba(0, 255, 255, 0.15);
  border-color: #00ffff;
  text-shadow: 
    0 0 10px #00ffff,
    0 0 20px #00ffff;
  box-shadow: 
    0 0 20px rgba(0, 255, 255, 0.4),
    inset 0 0 15px rgba(0, 255, 255, 0.2);
  animation: xGlow 2s ease-in-out infinite alternate;
}

@keyframes xGlow {
  from { 
    box-shadow: 
      0 0 15px rgba(0, 255, 255, 0.3),
      inset 0 0 10px rgba(0, 255, 255, 0.15);
  }
  to { 
    box-shadow: 
      0 0 25px rgba(0, 255, 255, 0.6),
      inset 0 0 20px rgba(0, 255, 255, 0.3);
  }
}

.cell.o {
  color: #ff00ff;
  background: rgba(255, 0, 255, 0.15);
  border-color: #ff00ff;
  text-shadow: 
    0 0 10px #ff00ff,
    0 0 20px #ff00ff;
  box-shadow: 
    0 0 20px rgba(255, 0, 255, 0.4),
    inset 0 0 15px rgba(255, 0, 255, 0.2);
  animation: oGlow 2s ease-in-out infinite alternate;
}

@keyframes oGlow {
  from { 
    box-shadow: 
      0 0 15px rgba(255, 0, 255, 0.3),
      inset 0 0 10px rgba(255, 0, 255, 0.15);
  }
  to { 
    box-shadow: 
      0 0 25px rgba(255, 0, 255, 0.6),
      inset 0 0 20px rgba(255, 0, 255, 0.3);
  }
}

.cell.winning {
  animation: winningPulse 0.8s ease-in-out infinite;
  background: linear-gradient(135deg, rgba(0, 255, 255, 0.3), rgba(255, 0, 255, 0.3)) !important;
  border-color: #fff !important;
  box-shadow: 
    0 0 30px rgba(255, 255, 255, 0.6),
    inset 0 0 20px rgba(255, 255, 255, 0.3) !important;
  position: relative;
}

.cell.winning::after {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(90deg, 
    transparent, 
    rgba(255, 255, 255, 0.8), 
    transparent
  );
  border-radius: 10px;
  animation: borderLight 1.5s linear infinite;
}

@keyframes winningPulse {
  0%, 100% { 
    transform: scale(1);
    box-shadow: 0 0 25px rgba(255, 255, 255, 0.5);
  }
  50% { 
    transform: scale(1.08);
    box-shadow: 0 0 40px rgba(255, 255, 255, 0.7);
  }
}

@keyframes neonRunningLight {
  0% {
    filter: hue-rotate(0deg) brightness(1.2);
  }
  100% {
    filter: hue-rotate(360deg) brightness(1.2);
  }
}

@keyframes borderLight {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100%);
  }
}

#status {
  text-align: center;
  font-size: 1.5em;
  color: #00ffff;
  margin: 20px 0;
  min-height: 50px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 3px;
  padding: 15px 30px;
  background: rgba(0, 255, 255, 0.05);
  border: 1px solid rgba(0, 255, 255, 0.3);
  border-radius: 10px;
  box-shadow: 
    0 0 20px rgba(0, 255, 255, 0.2),
    inset 0 0 20px rgba(0, 255, 255, 0.05);
  text-shadow: 0 0 10px #00ffff;
  position: relative;
  overflow: hidden;
  animation: statusFade 2s ease-in-out infinite;
}

#status::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(0, 255, 255, 0.3), transparent);
  animation: statusScan 3s linear infinite;
}

@keyframes statusScan {
  0% { left: -100%; }
  100% { left: 100%; }
}

@keyframes statusFade {
  0%, 100% {
    opacity: 0.9;
  }
  50% {
    opacity: 1;
  }
}

#controls {
  display: flex;
  flex-direction: column;
  gap: 15px;
  margin-top: 30px;
}

.button-group {
  display: flex;
  gap: 10px;
  justify-content: center;
}

button {
  padding: 15px 30px;
  font-size: 1em;
  border: 2px solid rgba(0, 255, 255, 0.5);
  border-radius: 10px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.3s ease;
  flex: 1;
  background: rgba(0, 255, 255, 0.05);
  color: #00ffff;
  text-transform: uppercase;
  letter-spacing: 2px;
  position: relative;
  overflow: hidden;
  box-shadow: 
    0 0 20px rgba(0, 255, 255, 0.2),
    inset 0 0 20px rgba(0, 255, 255, 0.05);
  text-shadow: 0 0 5px #00ffff;
  touch-action: manipulation;
  -webkit-tap-highlight-color: transparent;
  user-select: none;
  -webkit-user-select: none;
  will-change: transform;
}

button::before {
  content: '';
  position: absolute;
  top: 50%;
  left: 50%;
  width: 0;
  height: 0;
  border-radius: 50%;
  background: rgba(0, 255, 255, 0.3);
  transform: translate(-50%, -50%);
  transition: width 0.6s, height 0.6s;
}

button:hover::before {
  width: 300px;
  height: 300px;
}

button:hover {
  transform: translateY(-2px);
  border-color: #00ffff;
  box-shadow: 
    0 0 20px rgba(0, 255, 255, 0.4),
    inset 0 0 20px rgba(0, 255, 255, 0.15);
  background: rgba(0, 255, 255, 0.1);
}

button:active {
  transform: translateY(-1px);
  box-shadow: 
    0 0 40px rgba(255, 255, 255, 0.8),
    inset 0 0 20px rgba(255, 255, 255, 0.3);
}

#resetBtn {
  border-color: rgba(255, 0, 255, 0.5);
  color: #ff00ff;
  text-shadow: 0 0 5px #ff00ff;
}

#resetBtn::before {
  background: rgba(255, 0, 255, 0.3);
}

#resetBtn:hover {
  border-color: #ff00ff;
  box-shadow: 
    0 0 30px rgba(255, 0, 255, 0.5),
    inset 0 0 30px rgba(255, 0, 255, 0.2);
  background: rgba(255, 0, 255, 0.15);
}

.difficulty-btn.active {
  background: rgba(0, 255, 255, 0.2);
  border-color: #00ffff;
  box-shadow: 
    0 0 30px rgba(0, 255, 255, 0.6),
    inset 0 0 20px rgba(0, 255, 255, 0.3);
}

#scoreBoard {
  display: flex;
  justify-content: space-around;
  margin: 20px 0;
  padding: 20px;
  background: rgba(0, 0, 0, 0.3);
  border-radius: 10px;
  border: 1px solid rgba(0, 255, 255, 0.2);
  box-shadow: inset 0 0 20px rgba(0, 255, 255, 0.05);
}

.score {
  text-align: center;
  padding: 10px 20px;
  border-radius: 8px;
  background: rgba(0, 255, 255, 0.05);
  border: 1px solid rgba(0, 255, 255, 0.2);
}

.score-label {
  font-size: 0.85em;
  color: #00ffff;
  margin-bottom: 8px;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-shadow: 0 0 5px #00ffff;
}

.score-value {
  font-size: 2em;
  font-weight: bold;
  color: #ff00ff;
  text-shadow: 
    0 0 10px #ff00ff,
    0 0 20px #ff00ff;
}

#aiThinking {
  text-align: center;
  color: #ff00ff;
  font-style: italic;
  display: none;
  animation: blink 1s infinite;
  text-transform: uppercase;
  letter-spacing: 3px;
  text-shadow: 0 0 10px #ff00ff;
  font-size: 1.1em;
  padding: 10px;
  background: rgba(255, 0, 255, 0.05);
  border-radius: 8px;
  border: 1px solid rgba(255, 0, 255, 0.2);
}

#hintMessage {
  text-align: center;
  color: #00ffff;
  font-size: 0.9em;
  margin: 10px 0;
  min-height: 25px;
  text-shadow: 0 0 5px #00ffff;
  letter-spacing: 1px;
}

.cell.hint {
  animation: hintPulse 1s ease-in-out infinite;
  border-color: #fff !important;
}

@keyframes hintPulse {
  0%, 100% { 
    transform: scale(1);
    box-shadow: 
      0 0 30px rgba(255, 255, 255, 0.6),
      inset 0 0 20px rgba(255, 255, 255, 0.2);
    border-color: rgba(255, 255, 255, 0.6);
  }
  50% { 
    transform: scale(1.08);
    box-shadow: 
      0 0 50px rgba(255, 255, 255, 1),
      inset 0 0 30px rgba(255, 255, 255, 0.4);
    border-color: rgba(255, 255, 255, 1);
  }
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

#credits {
  margin-top: 30px;
  padding-top: 20px;
  border-top: 1px solid rgba(0, 255, 255, 0.2);
  text-align: center;
}

#credits p {
  color: rgba(0, 255, 255, 0.6);
  font-size: 0.8em;
  margin: 5px 0;
  letter-spacing: 1px;
}

#credits a {
  color: #00ffff;
  text-decoration: none;
  transition: all 0.3s ease;
  text-shadow: 0 0 5px rgba(0, 255, 255, 0.5);
}

#credits a:hover {
  color: #ff00ff;
  text-shadow: 0 0 10px rgba(255, 0, 255, 0.8);
}

@media (max-width: 600px) {
  body {
    padding: 10px;
    width: 100vw;
    height: 100vh;
  }
  
  #gameContainer {
    padding: 20px 15px;
    max-width: 100%;
    width: calc(100% - 20px);
  }
  
  h1 {
    font-size: 1.3em;
    letter-spacing: 2px;
    margin-bottom: 8px;
    animation: none;
    text-shadow: 0 0 10px #00ffff;
  }
  
  .subtitle {
    font-size: 0.75em;
    margin-bottom: 15px;
    text-shadow: 0 0 5px #ff00ff;
  }
  
  #gameBoard {
    gap: 10px;
    padding: 15px;
    max-width: 100%;
    box-shadow: none;
  }
  
  .cell {
    font-size: 2.2em;
    border-width: 2px;
    animation: none;
    box-shadow: 0 0 10px rgba(0, 255, 255, 0.2);
  }
  
  .cell:hover:not(.taken) {
    animation: none;
    transform: none;
    box-shadow: 0 0 15px rgba(0, 255, 255, 0.4);
  }
  
  .cell.x {
    animation: none;
    filter: none;
    text-shadow: 0 0 8px #00ffff;
    box-shadow: 0 0 12px rgba(0, 255, 255, 0.4);
  }
  
  .cell.o {
    animation: none;
    filter: none;
    text-shadow: 0 0 8px #ff00ff;
    box-shadow: 0 0 12px rgba(255, 0, 255, 0.4);
  }
  
  .cell.winning {
    animation: winningPulse 0.8s ease-in-out 3;
  }
  
  .cell.winning::after {
    display: none;
  }
  
  #status::before {
    display: none;
  }
  
  #status {
    animation: none;
    font-size: 1em;
    letter-spacing: 1px;
    padding: 12px 15px;
    box-shadow: none;
  }
  
  body::before {
    opacity: 0.2;
    animation: none;
  }
  
  button::before {
    display: none;
  }
  
  button {
    padding: 12px 15px;
    font-size: 0.75em;
    letter-spacing: 1px;
    box-shadow: 0 0 10px rgba(0, 255, 255, 0.15);
  }
  
  button:hover {
    transform: none;
    box-shadow: 0 0 15px rgba(0, 255, 255, 0.3);
  }
  
  #scoreBoard {
    padding: 15px 10px;
    margin: 15px 0;
    box-shadow: none;
  }
  
  .score {
    padding: 8px 12px;
    box-shadow: none;
  }
  
  .score-label {
    font-size: 0.7em;
    margin-bottom: 5px;
    text-shadow: 0 0 3px #00ffff;
  }
  
  .score-value {
    font-size: 1.5em;
    text-shadow: 0 0 5px #ff00ff;
  }
  
  #hintMessage {
    font-size: 0.8em;
    text-shadow: 0 0 3px #00ffff;
  }
  
  #aiThinking {
    font-size: 0.9em;
    padding: 8px;
    text-shadow: 0 0 5px #ff00ff;
  }
  
  .button-group {
    gap: 8px;
  }
  
  #controls {
    gap: 10px;
  }
  
  #credits {
    margin-top: 20px;
    padding-top: 15px;
  }
  
  #credits p {
    font-size: 0.7em;
  }
  
  #credits a {
    text-shadow: 0 0 3px currentColor;
  }
}

@media (max-width: 400px) {
  #gameContainer {
    padding: 15px 10px;
  }
  
  h1 {
    font-size: 0.7em;
    letter-spacing: 1px;
  }
  
  .cell {
    font-size: 1.7em;
  }
  
  button {
    padding: 10px 12px;
    font-size: 0.7em;
  }
}

@media (min-width: 601px) and (max-width: 1024px) {
  #gameContainer {
    max-width: 550px;
  }
  
  .cell {
    font-size: 3.5em;
  }
  
  button {
    font-size: 0.95em;
  }
}
</style>
</head>
<body>
<div id="gameContainer">
  <h1>⭕ TIC TAC TOE ❌</h1>
  <p class="subtitle">Generator Solver</p>
  
  <div id="scoreBoard">
    <div class="score">
      <div class="score-label">Player (X)</div>
      <div class="score-value" id="playerScore">0</div>
    </div>
    <div class="score">
      <div class="score-label">Draws</div>
      <div class="score-value" id="drawScore">0</div>
    </div>
    <div class="score">
      <div class="score-label">AI (O)</div>
      <div class="score-value" id="aiScore">0</div>
    </div>
  </div>
  
  <div id="status">Your turn! Click any cell to start</div>
  <div id="aiThinking">AI is thinking...</div>
  <div id="hintMessage">💡 Hint: Click "Show Best Move" to see optimal play</div>
  
  <div id="gameBoard"></div>
  
  <div id="controls">
    <div class="button-group">
      <button id="undoBtn" class="difficulty-btn">Undo Move</button>
      <button id="hintBtn" class="difficulty-btn">Get Hint</button>
    </div>
    <div class="button-group">
      <button id="autoSolveBtn" class="difficulty-btn">Auto Solve</button>
      <button id="resetBtn">Restart Game</button>
    </div>
  </div>
  
  <div id="credits">
    <p>Created by <a href="https://x.com/owsnpidc" target="_blank">Zayn🐬</a></p>
    <p>Inspired by <a href="https://x.com/SoundnessLabs" target="_blank">Soundness</a></p>
  </div>
</div>

<script>
class TicTacToeSolver {
  constructor() {
    this.board = Array(9).fill(null);
    this.currentPlayer = 'X';
    this.gameActive = true;
    this.difficulty = 'easy';
    this.autoPlay = false;
    this.moveHistory = [];
    this.scores = {
      player: 0,
      ai: 0,
      draw: 0
    };
    
    this.createParticles();
    
    this.winPatterns = [
      [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
      [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
      [0, 4, 8], [2, 4, 6]             // Diagonals
    ];
    
    this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
    
    this.loadScores();
    this.initializeBoard();
    this.setupEventListeners();
  }
  
  initializeBoard() {
    const gameBoard = document.getElementById('gameBoard');
    gameBoard.innerHTML = '';
    
    for (let i = 0; i < 9; i++) {
      const cell = document.createElement('button');
      cell.className = 'cell';
      cell.dataset.index = i;
      
      // Support both click and touch events
      cell.addEventListener('click', (e) => {
        e.preventDefault();
        this.handleCellClick(i);
      });
      
      cell.addEventListener('touchend', (e) => {
        e.preventDefault();
        this.handleCellClick(i);
      }, { passive: false });
      
      gameBoard.appendChild(cell);
    }
  }
  
  setupEventListeners() {
    // Reset button
    const resetBtn = document.getElementById('resetBtn');
    resetBtn.addEventListener('click', (e) => {
      e.preventDefault();
      this.resetGame();
    });
    resetBtn.addEventListener('touchend', (e) => {
      e.preventDefault();
      this.resetGame();
    }, { passive: false });
    
    // Hint button
    const hintBtn = document.getElementById('hintBtn');
    hintBtn.addEventListener('click', (e) => {
      e.preventDefault();
      this.showHint();
    });
    hintBtn.addEventListener('touchend', (e) => {
      e.preventDefault();
      this.showHint();
    }, { passive: false });
    
    // Undo button
    const undoBtn = document.getElementById('undoBtn');
    undoBtn.addEventListener('click', (e) => {
      e.preventDefault();
      this.undoMove();
    });
    undoBtn.addEventListener('touchend', (e) => {
      e.preventDefault();
      this.undoMove();
    }, { passive: false });
    
    // Auto solve button
    const autoSolveBtn = document.getElementById('autoSolveBtn');
    autoSolveBtn.addEventListener('click', (e) => {
      e.preventDefault();
      this.autoSolve();
    });
    autoSolveBtn.addEventListener('touchend', (e) => {
      e.preventDefault();
      this.autoSolve();
    }, { passive: false });
  }
  
  createParticles() {
    const container = document.body;
    const isMobile = window.innerWidth <= 600;
    const particleCount = isMobile ? 5 : 15;
    
    for (let i = 0; i < particleCount; i++) {
      const particle = document.createElement('div');
      particle.className = 'particle';
      particle.style.left = Math.random() * 100 + '%';
      particle.style.animationDelay = Math.random() * 8 + 's';
      particle.style.animationDuration = (8 + Math.random() * 4) + 's';
      container.appendChild(particle);
    }
  }
  
  handleCellClick(index) {
    if (!this.gameActive || this.board[index] !== null || this.currentPlayer !== 'X') {
      return;
    }
    
    this.clearHints();
    this.moveHistory.push({ index, player: 'X', board: [...this.board] });
    this.makeMove(index, 'X');
    this.playSound(523, 0.15);
    
    if (this.gameActive && !this.checkWinner()) {
      this.currentPlayer = 'O';
      this.updateStatus("O's Turn...");
      document.getElementById('aiThinking').style.display = 'block';
      
      setTimeout(() => {
        this.aiMove();
        document.getElementById('aiThinking').style.display = 'none';
      }, 500);
    }
  }
  
  updateStatus(message) {
    const status = document.getElementById('status');
    status.style.animation = 'none';
    setTimeout(() => {
      status.textContent = message;
      status.style.animation = 'statusFade 2s ease-in-out infinite';
    }, 10);
  }
  
  makeMove(index, player) {
    this.board[index] = player;
    const cell = document.querySelector(`[data-index="${index}"]`);
    cell.textContent = player;
    cell.classList.add('taken', player.toLowerCase());
    
    const winner = this.checkWinner();
    if (winner) {
      this.endGame(winner);
    } else if (this.board.every(cell => cell !== null)) {
      this.endGame('draw');
    }
  }
  
  aiMove() {
    let move = this.getRandomMove();
    
    this.moveHistory.push({ index: move, player: 'O', board: [...this.board] });
    this.makeMove(move, 'O');
    this.playSound(392, 0.15);
    this.currentPlayer = 'X';
    
    if (this.gameActive) {
      this.updateStatus("X's Turn");
    }
  }
  
  getBestMove() {
    let bestScore = -Infinity;
    let bestMove = 0;
    
    // First move optimization
    if (this.board.filter(cell => cell !== null).length === 1) {
      const corners = [0, 2, 6, 8];
      const center = 4;
      if (this.board[center] === null) return center;
      return corners.find(i => this.board[i] === null);
    }
    
    for (let i = 0; i < 9; i++) {
      if (this.board[i] === null) {
        this.board[i] = 'O';
        const score = this.minimax(this.board, 0, false);
        this.board[i] = null;
        
        if (score > bestScore) {
          bestScore = score;
          bestMove = i;
        }
      }
    }
    
    return bestMove;
  }
  
  minimax(board, depth, isMaximizing) {
    const winner = this.checkWinnerForBoard(board);
    
    if (winner === 'O') return 10 - depth;
    if (winner === 'X') return depth - 10;
    if (board.every(cell => cell !== null)) return 0;
    
    if (isMaximizing) {
      let bestScore = -Infinity;
      for (let i = 0; i < 9; i++) {
        if (board[i] === null) {
          board[i] = 'O';
          const score = this.minimax(board, depth + 1, false);
          board[i] = null;
          bestScore = Math.max(score, bestScore);
        }
      }
      return bestScore;
    } else {
      let bestScore = Infinity;
      for (let i = 0; i < 9; i++) {
        if (board[i] === null) {
          board[i] = 'X';
          const score = this.minimax(board, depth + 1, true);
          board[i] = null;
          bestScore = Math.min(score, bestScore);
        }
      }
      return bestScore;
    }
  }
  
  getRandomMove() {
    const availableMoves = this.board
      .map((cell, index) => cell === null ? index : null)
      .filter(index => index !== null);
    return availableMoves[Math.floor(Math.random() * availableMoves.length)];
  }
  
  checkWinner() {
    return this.checkWinnerForBoard(this.board);
  }
  
  checkWinnerForBoard(board) {
    for (const pattern of this.winPatterns) {
      const [a, b, c] = pattern;
      if (board[a] && board[a] === board[b] && board[a] === board[c]) {
        return board[a];
      }
    }
    return null;
  }
  
  endGame(result) {
    this.gameActive = false;
    
    if (result === 'draw') {
      this.updateStatus("It's a Draw! 🤝 - Starting new game...");
      this.scores.draw++;
      this.playSound(349, 0.3);
      document.getElementById('hintMessage').textContent = "🤝 Game ended in a draw!";
    } else {
      const winningPattern = this.winPatterns.find(pattern => {
        const [a, b, c] = pattern;
        return this.board[a] === result && this.board[b] === result && this.board[c] === result;
      });
      
      if (winningPattern) {
        winningPattern.forEach(index => {
          document.querySelector(`[data-index="${index}"]`).classList.add('winning');
        });
      }
      
      if (result === 'X') {
        this.updateStatus("X Wins! 🎉 - Starting new game...");
        this.scores.player++;
        this.playSound(523, 0.4);
        document.getElementById('hintMessage').textContent = "🎉 Congratulations! You won!";
      } else {
        this.updateStatus("O Wins! 🤖 - Starting new game...");
        this.scores.ai++;
        this.playSound(262, 0.4);
        document.getElementById('hintMessage').textContent = "🤖 AI wins this round!";
      }
    }
    
    this.updateScoreDisplay();
    this.saveScores();
    
    // Auto start new game after 2 seconds
    setTimeout(() => {
      this.startNewRound();
    }, 2000);
  }
  
  startNewRound() {
    this.board = Array(9).fill(null);
    this.currentPlayer = 'X';
    this.gameActive = true;
    this.moveHistory = [];
    
    document.querySelectorAll('.cell').forEach(cell => {
      cell.textContent = '';
      cell.classList.remove('taken', 'x', 'o', 'winning', 'hint');
    });
    
    this.updateStatus("X's Turn - Click any cell to start");
    document.getElementById('aiThinking').style.display = 'none';
    document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
    
    this.playSound(440, 0.12);
  }
  
  showHint() {
    if (!this.gameActive || this.currentPlayer !== 'X') {
      document.getElementById('hintMessage').textContent = "⚠️ Can only show hints on your turn!";
      this.playSound(294, 0.1);
      return;
    }
    
    this.clearHints();
    const bestMove = this.getBestMoveForPlayer('X');
    
    if (bestMove !== null) {
      const cell = document.querySelector(`[data-index="${bestMove}"]`);
      cell.classList.add('hint');
      
      const analysis = this.analyzeMove(bestMove);
      document.getElementById('hintMessage').textContent = `💡 ${analysis}`;
      this.playSound(659, 0.12);
      
      setTimeout(() => {
        this.clearHints();
        document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
      }, 3000);
    }
  }
  
  undoMove() {
    if (this.moveHistory.length < 2 || !this.gameActive) {
      document.getElementById('hintMessage').textContent = "⚠️ No moves to undo!";
      this.playSound(294, 0.1);
      setTimeout(() => {
        document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
      }, 2000);
      return;
    }
    
    this.playSound(440, 0.12);
    
    // Undo last two moves (player and AI)
    this.moveHistory.pop();
    this.moveHistory.pop();
    
    if (this.moveHistory.length > 0) {
      const lastState = this.moveHistory[this.moveHistory.length - 1];
      this.board = [...lastState.board];
    } else {
      this.board = Array(9).fill(null);
    }
    
    this.currentPlayer = 'X';
    this.gameActive = true;
    
    // Update UI
    document.querySelectorAll('.cell').forEach((cell, index) => {
      cell.textContent = this.board[index] || '';
      cell.classList.remove('taken', 'x', 'o', 'winning', 'hint');
      if (this.board[index]) {
        cell.classList.add('taken', this.board[index].toLowerCase());
      }
    });
    
    this.updateStatus("X's Turn");
    document.getElementById('hintMessage').textContent = "⏪ Move undone!";
    this.playSound(349, 0.15);
    
    setTimeout(() => {
      document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
    }, 2000);
  }
  
  autoSolve() {
    if (!this.gameActive || this.currentPlayer !== 'X') {
      document.getElementById('hintMessage').textContent = "⚠️ Can only auto-solve on your turn!";
      setTimeout(() => {
        document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
      }, 2000);
      return;
    }
    
    this.clearHints();
    const bestMove = this.getBestMoveForPlayer('X');
    
    if (bestMove !== null && bestMove !== undefined) {
      const cell = document.querySelector(`[data-index="${bestMove}"]`);
      if (cell && !cell.classList.contains('taken')) {
        cell.classList.add('hint');
        
        setTimeout(() => {
          cell.classList.remove('hint');
          
          // Execute the move directly
          this.clearHints();
          this.moveHistory.push({ index: bestMove, player: 'X', board: [...this.board] });
          this.makeMove(bestMove, 'X');
          this.playSound(587, 0.15);
          
          setTimeout(() => {
            this.playSound(659, 0.12);
          }, 150);
          
          document.getElementById('hintMessage').textContent = "🤖 Auto-solved optimal move!";
          
          if (this.gameActive && !this.checkWinner()) {
            this.currentPlayer = 'O';
            this.updateStatus("O's Turn...");
            document.getElementById('aiThinking').style.display = 'block';
            
            setTimeout(() => {
              this.aiMove();
              document.getElementById('aiThinking').style.display = 'none';
              
              setTimeout(() => {
                if (this.gameActive) {
                  document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
                }
              }, 2000);
            }, 500);
          }
        }, 600);
      }
    }
  }
  
  analyzeMove(index) {
    // Check if move wins
    this.board[index] = 'X';
    if (this.checkWinner() === 'X') {
      this.board[index] = null;
      return "Winning move! Click the highlighted cell to win! 🎉";
    }
    this.board[index] = null;
    
    // Check if move blocks AI win
    this.board[index] = 'O';
    if (this.checkWinner() === 'O') {
      this.board[index] = null;
      return "Defensive move! Blocks AI from winning 🛡️";
    }
    this.board[index] = null;
    
    // Check if center
    if (index === 4) {
      return "Strategic center control! 🎯";
    }
    
    // Check if corner
    if ([0, 2, 6, 8].includes(index)) {
      return "Strong corner position! 💪";
    }
    
    return "Best available move 👍";
  }
  
  getBestMoveForPlayer(player) {
    let bestScore = -Infinity;
    let bestMove = null;
    
    // Check for immediate winning move
    for (let i = 0; i < 9; i++) {
      if (this.board[i] === null) {
        this.board[i] = player;
        if (this.checkWinner() === player) {
          this.board[i] = null;
          return i;
        }
        this.board[i] = null;
      }
    }
    
    // Check for blocking opponent's winning move
    const opponent = player === 'X' ? 'O' : 'X';
    for (let i = 0; i < 9; i++) {
      if (this.board[i] === null) {
        this.board[i] = opponent;
        if (this.checkWinner() === opponent) {
          this.board[i] = null;
          return i;
        }
        this.board[i] = null;
      }
    }
    
    // Use minimax for best strategic move
    for (let i = 0; i < 9; i++) {
      if (this.board[i] === null) {
        this.board[i] = player;
        const score = this.minimaxForPlayer(this.board, 0, false, player);
        this.board[i] = null;
        
        if (score > bestScore) {
          bestScore = score;
          bestMove = i;
        }
      }
    }
    
    return bestMove !== null ? bestMove : this.getRandomMove();
  }
  
  minimaxForPlayer(board, depth, isMaximizing, player) {
    const winner = this.checkWinnerForBoard(board);
    
    if (winner === player) return 10 - depth;
    if (winner && winner !== player) return depth - 10;
    if (board.every(cell => cell !== null)) return 0;
    
    const opponent = player === 'X' ? 'O' : 'X';
    
    if (isMaximizing) {
      let bestScore = -Infinity;
      for (let i = 0; i < 9; i++) {
        if (board[i] === null) {
          board[i] = player;
          const score = this.minimaxForPlayer(board, depth + 1, false, player);
          board[i] = null;
          bestScore = Math.max(score, bestScore);
        }
      }
      return bestScore;
    } else {
      let bestScore = Infinity;
      for (let i = 0; i < 9; i++) {
        if (board[i] === null) {
          board[i] = opponent;
          const score = this.minimaxForPlayer(board, depth + 1, true, player);
          board[i] = null;
          bestScore = Math.min(score, bestScore);
        }
      }
      return bestScore;
    }
  }
  
  clearHints() {
    document.querySelectorAll('.cell').forEach(cell => {
      cell.classList.remove('hint');
    });
  }
  
  
  
  resetGame() {
    this.board = Array(9).fill(null);
    this.currentPlayer = 'X';
    this.gameActive = true;
    this.moveHistory = [];
    
    // Reset scores to zero
    this.scores = {
      player: 0,
      ai: 0,
      draw: 0
    };
    this.updateScoreDisplay();
    this.saveScores();
    
    document.querySelectorAll('.cell').forEach(cell => {
      cell.textContent = '';
      cell.classList.remove('taken', 'x', 'o', 'winning', 'hint');
    });
    
    this.updateStatus("X's Turn - Click any cell to start");
    document.getElementById('aiThinking').style.display = 'none';
    document.getElementById('hintMessage').textContent = "💡 Hint: Click 'Get Hint' to see optimal play";
    
    this.playSound(349, 0.18);
  }
  
  updateScoreDisplay() {
    document.getElementById('playerScore').textContent = this.scores.player;
    document.getElementById('aiScore').textContent = this.scores.ai;
    document.getElementById('drawScore').textContent = this.scores.draw;
  }
  
  saveScores() {
    localStorage.setItem('tictactoe_scores', JSON.stringify(this.scores));
  }
  
  loadScores() {
    const saved = localStorage.getItem('tictactoe_scores');
    if (saved) {
      this.scores = JSON.parse(saved);
      this.updateScoreDisplay();
    }
  }
  
  playSound(frequency, duration) {
    try {
      const oscillator = this.audioContext.createOscillator();
      const gainNode = this.audioContext.createGain();
      
      oscillator.connect(gainNode);
      gainNode.connect(this.audioContext.destination);
      
      oscillator.frequency.value = frequency;
      oscillator.type = 'sine';
      
      gainNode.gain.setValueAtTime(0.3, this.audioContext.currentTime);
      gainNode.gain.exponentialRampToValueAtTime(0.01, this.audioContext.currentTime + duration);
      
      oscillator.start(this.audioContext.currentTime);
      oscillator.stop(this.audioContext.currentTime + duration);
    } catch (error) {
      console.log('Audio error:', error);
    }
  }
}

// Initialize game when DOM is loaded
window.addEventListener('DOMContentLoaded', () => {
  new TicTacToeSolver();
});
</script>
</body>
</html>
