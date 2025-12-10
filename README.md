# ?
Something...
Below is `deepseek` wordle so if you wanna play, do so!

















`
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wordle Game</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #121213;
            color: #ffffff;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }
        
        .container {
            max-width: 500px;
            width: 100%;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            width: 100%;
            padding-bottom: 20px;
            border-bottom: 1px solid #3a3a3c;
            margin-bottom: 20px;
        }
        
        h1 {
            font-size: 2.5rem;
            letter-spacing: 5px;
            text-align: center;
            color: #ffffff;
        }
        
        .game-info {
            display: flex;
            gap: 15px;
        }
        
        .game-info button {
            background-color: #818384;
            color: white;
            border: none;
            border-radius: 5px;
            padding: 8px 12px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.2s;
        }
        
        .game-info button:hover {
            background-color: #6a6a6c;
        }
        
        .stats {
            background-color: #3a3a3c;
            padding: 5px 10px;
            border-radius: 5px;
            font-weight: bold;
        }
        
        .game-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            width: 100%;
            gap: 20px;
        }
        
        .message {
            height: 30px;
            font-weight: bold;
            text-align: center;
            margin: 10px 0;
        }
        
        .success {
            color: #6aaa64;
        }
        
        .error {
            color: #ff6b6b;
        }
        
        .board {
            display: grid;
            grid-template-rows: repeat(6, 1fr);
            gap: 8px;
            width: 350px;
            height: 420px;
            margin-bottom: 20px;
        }
        
        .row {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 8px;
        }
        
        .tile {
            width: 100%;
            height: 100%;
            border: 2px solid #3a3a3c;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 2rem;
            font-weight: bold;
            text-transform: uppercase;
            user-select: none;
            transition: transform 0.2s;
        }
        
        .tile.filled {
            border-color: #565758;
            animation: pop 0.1s;
        }
        
        @keyframes pop {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        
        .tile.correct {
            background-color: #6aaa64;
            border-color: #6aaa64;
            color: white;
        }
        
        .tile.present {
            background-color: #c9b458;
            border-color: #c9b458;
            color: white;
        }
        
        .tile.absent {
            background-color: #3a3a3c;
            border-color: #3a3a3c;
            color: white;
        }
        
        .tile.wrong-position {
            animation: shake 0.5s;
        }
        
        @keyframes shake {
            0%, 100% { transform: translateX(0); }
            20%, 60% { transform: translateX(-5px); }
            40%, 80% { transform: translateX(5px); }
        }
        
        .keyboard {
            display: flex;
            flex-direction: column;
            gap: 8px;
            width: 100%;
            max-width: 500px;
        }
        
        .keyboard-row {
            display: flex;
            justify-content: center;
            gap: 6px;
        }
        
        .key {
            background-color: #818384;
            color: white;
            border: none;
            border-radius: 4px;
            height: 58px;
            min-width: 40px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            text-transform: uppercase;
            user-select: none;
            flex: 1;
            transition: background-color 0.2s;
        }
        
        .key:hover {
            background-color: #6a6a6c;
        }
        
        .key.wide {
            flex: 1.5;
            font-size: 0.8rem;
        }
        
        .key.correct {
            background-color: #6aaa64;
        }
        
        .key.present {
            background-color: #c9b458;
        }
        
        .key.absent {
            background-color: #3a3a3c;
        }
        
        .instructions {
            background-color: #3a3a3c;
            padding: 20px;
            border-radius: 10px;
            margin-top: 30px;
            width: 100%;
            max-width: 500px;
        }
        
        .instructions h3 {
            margin-bottom: 15px;
            color: #ffffff;
        }
        
        .instructions p {
            margin-bottom: 15px;
            line-height: 1.5;
        }
        
        .example {
            display: flex;
            gap: 5px;
            margin-bottom: 15px;
        }
        
        .example .tile {
            width: 40px;
            height: 40px;
            font-size: 1.2rem;
        }
        
        .instructions ul {
            padding-left: 20px;
            margin-bottom: 15px;
        }
        
        .instructions li {
            margin-bottom: 8px;
        }
        
        @media (max-width: 500px) {
            .board {
                width: 300px;
                height: 360px;
            }
            
            .tile {
                font-size: 1.5rem;
            }
            
            .key {
                height: 50px;
                min-width: 30px;
                font-size: 0.9rem;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>WORDLE</h1>
            <div class="game-info">
                <div class="stats">
                    <span id="score">0</span> wins
                </div>
                <button id="help-btn">Help</button>
                <button id="new-game-btn">New Game</button>
            </div>
        </header>
        
        <div class="game-container">
            <div class="message" id="message"></div>
            
            <div class="board" id="board">
                <!-- Game board will be generated by JavaScript -->
            </div>
            
            <div class="keyboard">
                <div class="keyboard-row">
                    <div class="key" data-key="Q">Q</div>
                    <div class="key" data-key="W">W</div>
                    <div class="key" data-key="E">E</div>
                    <div class="key" data-key="R">R</div>
                    <div class="key" data-key="T">T</div>
                    <div class="key" data-key="Y">Y</div>
                    <div class="key" data-key="U">U</div>
                    <div class="key" data-key="I">I</div>
                    <div class="key" data-key="O">O</div>
                    <div class="key" data-key="P">P</div>
                </div>
                <div class="keyboard-row">
                    <div class="key" data-key="A">A</div>
                    <div class="key" data-key="S">S</div>
                    <div class="key" data-key="D">D</div>
                    <div class="key" data-key="F">F</div>
                    <div class="key" data-key="G">G</div>
                    <div class="key" data-key="H">H</div>
                    <div class="key" data-key="J">J</div>
                    <div class="key" data-key="K">K</div>
                    <div class="key" data-key="L">L</div>
                </div>
                <div class="keyboard-row">
                    <div class="key wide" id="enter">Enter</div>
                    <div class="key" data-key="Z">Z</div>
                    <div class="key" data-key="X">X</div>
                    <div class="key" data-key="C">C</div>
                    <div class="key" data-key="V">V</div>
                    <div class="key" data-key="B">B</div>
                    <div class="key" data-key="N">N</div>
                    <div class="key" data-key="M">M</div>
                    <div class="key wide" id="backspace">⌫</div>
                </div>
            </div>
        </div>
        
        <div class="instructions" id="instructions">
            <h3>How to Play</h3>
            <p>Guess the <strong>WORDLE</strong> in 6 tries.</p>
            <ul>
                <li>Each guess must be a valid 5-letter word.</li>
                <li>The color of the tiles will change to show how close your guess was to the word.</li>
            </ul>
            
            <p><strong>Examples</strong></p>
            <div class="example">
                <div class="tile correct">W</div>
                <div class="tile">E</div>
                <div class="tile">A</div>
                <div class="tile">R</div>
                <div class="tile">Y</div>
            </div>
            <p><strong>W</strong> is in the word and in the correct spot.</p>
            
            <div class="example">
                <div class="tile">P</div>
                <div class="tile present">I</div>
                <div class="tile">L</div>
                <div class="tile">L</div>
                <div class="tile">S</div>
            </div>
            <p><strong>I</strong> is in the word but in the wrong spot.</p>
            
            <div class="example">
                <div class="tile">V</div>
                <div class="tile">A</div>
                <div class="tile">G</div>
                <div class="tile absent">U</div>
                <div class="tile">E</div>
            </div>
            <p><strong>U</strong> is not in the word in any spot.</p>
            
            <p style="text-align: center; margin-top: 20px;">
                <button id="close-help" style="padding: 10px 20px; background-color: #6aaa64; color: white; border: none; border-radius: 5px; cursor: pointer;">Got it!</button>
            </p>
        </div>
    </div>

    <script>
        // Game state variables
        let currentRow = 0;
        let currentTile = 0;
        let gameOver = false;
        let score = 0;
        let wordOfTheDay = '';
        
        // Word list (5-letter words)
        const wordList = [
            'APPLE', 'BRAIN', 'CHAIR', 'DREAM', 'EARTH', 'FLAME', 'GRAPE', 'HEART', 'IMAGE', 'JUICE',
            'KNIFE', 'LEMON', 'MONEY', 'NIGHT', 'OCEAN', 'PIANO', 'QUIET', 'RIVER', 'SMILE', 'TABLE',
            'UNITY', 'VOICE', 'WATER', 'YOUTH', 'ZEBRA', 'ALERT', 'BEACH', 'CLOUD', 'DANCE', 'EAGLE',
            'FRUIT', 'GHOST', 'HONEY', 'IGLOO', 'JELLY', 'KOALA', 'LIGHT', 'MAGIC', 'NOVEL', 'OPERA',
            'PEARL', 'QUEEN', 'ROBOT', 'SHARK', 'TIGER', 'UMBRA', 'VIXEN', 'WHALE', 'XENON', 'YACHT',
            'SOCKS', 'HAPPY', 'STINK', 'POWER', 'LOADS', 'WORLD', 'FOXES', 'PARSA', 'EDDIE', 'DAWNS',
            'FAKES', 'READS', 'KINGS', 'AMONG', 'QUEEN', 'BERRY'
        ];
        
        // Initialize the game
        function initGame() {
            // Reset game state
            currentRow = 0;
            currentTile = 0;
            gameOver = false;
            
            // Select a random word
            wordOfTheDay = wordList[Math.floor(Math.random() * wordList.length)];
            
            // Clear message
            document.getElementById('message').textContent = '';
            document.getElementById('message').className = 'message';
            
            // Create the game board
            const board = document.getElementById('board');
            board.innerHTML = '';
            
            for (let row = 0; row < 6; row++) {
                const rowElement = document.createElement('div');
                rowElement.className = 'row';
                
                for (let tile = 0; tile < 5; tile++) {
                    const tileElement = document.createElement('div');
                    tileElement.className = 'tile';
                    tileElement.id = `tile-${row}-${tile}`;
                    rowElement.appendChild(tileElement);
                }
                
                board.appendChild(rowElement);
            }
            
            // Reset keyboard colors
            document.querySelectorAll('.key').forEach(key => {
                key.className = 'key';
                if (key.id === 'enter' || key.id === 'backspace') {
                    key.classList.add('wide');
                }
            });
            
            // Update score display
            document.getElementById('score').textContent = score;
            
            // Hide instructions by default
            document.getElementById('instructions').style.display = 'none';
            
            console.log('Word to guess:', wordOfTheDay); // For debugging
        }
        
        // Handle key press
        function handleKeyPress(key) {
            if (gameOver) return;
            
            const messageElement = document.getElementById('message');
            
            // Handle Enter key
            if (key === 'ENTER') {
                if (currentTile !== 5) {
                    showMessage('Not enough letters', 'error');
                    return;
                }
                
                // Get the current guess
                let guess = '';
                for (let i = 0; i < 5; i++) {
                    const tile = document.getElementById(`tile-${currentRow}-${i}`);
                    guess += tile.textContent;
                }
                
                // Check if the guess is in the word list
                if (!wordList.includes(guess)) {
                    showMessage('Not in word list', 'error');
                    shakeRow(currentRow);
                    return;
                }
                
                // Check the guess against the word
                checkGuess(guess);
                return;
            }
            
            // Handle Backspace key
            if (key === 'BACKSPACE') {
                if (currentTile === 0) return;
                
                currentTile--;
                const tile = document.getElementById(`tile-${currentRow}-${currentTile}`);
                tile.textContent = '';
                tile.classList.remove('filled');
                return;
            }
            
            // Handle letter keys
            if (/^[A-Z]$/.test(key)) {
                if (currentTile === 5) return;
                
                const tile = document.getElementById(`tile-${currentRow}-${currentTile}`);
                tile.textContent = key;
                tile.classList.add('filled');
                currentTile++;
            }
        }
        
        // Check the guess against the word
        function checkGuess(guess) {
            const word = wordOfTheDay;
            const row = currentRow;
            
            // Create arrays to track which letters have been matched
            const guessLetters = guess.split('');
            const wordLetters = word.split('');
            const result = new Array(5).fill('absent');
            
            // First pass: mark correct letters
            for (let i = 0; i < 5; i++) {
                if (guessLetters[i] === wordLetters[i]) {
                    result[i] = 'correct';
                    guessLetters[i] = null;
                    wordLetters[i] = null;
                }
            }
            
            // Second pass: mark present letters
            for (let i = 0; i < 5; i++) {
                if (guessLetters[i] === null) continue;
                
                const index = wordLetters.indexOf(guessLetters[i]);
                if (index !== -1) {
                    result[i] = 'present';
                    wordLetters[index] = null;
                    guessLetters[i] = null;
                }
            }
            
            // Update tile colors
            let allCorrect = true;
            for (let i = 0; i < 5; i++) {
                const tile = document.getElementById(`tile-${row}-${i}`);
                
                // Add color with delay for animation effect
                setTimeout(() => {
                    tile.classList.add(result[i]);
                    
                    // Update keyboard key color
                    const key = document.querySelector(`.key[data-key="${tile.textContent}"]`);
                    if (key) {
                        // Only update if the new status is "higher" than current
                        const currentStatus = key.classList.contains('correct') ? 'correct' : 
                                             key.classList.contains('present') ? 'present' : 'absent';
                        
                        const newStatus = result[i];
                        
                        if (newStatus === 'correct' || 
                            (newStatus === 'present' && currentStatus !== 'correct') ||
                            (newStatus === 'absent' && currentStatus === 'absent')) {
                            
                            key.classList.remove('correct', 'present', 'absent');
                            key.classList.add(newStatus);
                        }
                    }
                }, i * 300);
                
                if (result[i] !== 'correct') {
                    allCorrect = false;
                }
            }
            
            // Move to next row
            currentRow++;
            currentTile = 0;
            
            // Check if the player won
            if (allCorrect) {
                gameOver = true;
                score++;
                document.getElementById('score').textContent = score;
                
                setTimeout(() => {
                    showMessage(`Congratulations! You guessed the word!`, 'success');
                }, 1500);
                
                return;
            }
            
            // Check if the game is over (no more rows)
            if (currentRow === 6) {
                gameOver = true;
                setTimeout(() => {
                    showMessage(`Game Over! The word was ${wordOfTheDay}`, 'error');
                }, 1500);
            }
        }
        
        // Show a message to the player
        function showMessage(text, type) {
            const messageElement = document.getElementById('message');
            messageElement.textContent = text;
            messageElement.className = 'message ' + type;
            
            // Clear message after 3 seconds
            setTimeout(() => {
                messageElement.textContent = '';
                messageElement.className = 'message';
            }, 3000);
        }
        
        // Shake row animation for invalid words
        function shakeRow(row) {
            for (let i = 0; i < 5; i++) {
                const tile = document.getElementById(`tile-${row}-${i}`);
                tile.classList.add('wrong-position');
                
                setTimeout(() => {
                    tile.classList.remove('wrong-position');
                }, 500);
            }
        }
        
        // Event listeners
        document.addEventListener('DOMContentLoaded', () => {
            // Initialize the game
            initGame();
            
            // Keyboard click events
            document.querySelectorAll('.key').forEach(key => {
                key.addEventListener('click', () => {
                    if (key.id === 'enter') {
                        handleKeyPress('ENTER');
                    } else if (key.id === 'backspace') {
                        handleKeyPress('BACKSPACE');
                    } else {
                        handleKeyPress(key.textContent);
                    }
                });
            });
            
            // Physical keyboard events
            document.addEventListener('keydown', (e) => {
                if (gameOver) return;
                
                const key = e.key.toUpperCase();
                
                if (key === 'ENTER') {
                    handleKeyPress('ENTER');
                } else if (key === 'BACKSPACE' || key === 'DELETE') {
                    handleKeyPress('BACKSPACE');
                } else if (/^[A-Z]$/.test(key)) {
                    handleKeyPress(key);
                }
            });
            
            // New game button
            document.getElementById('new-game-btn').addEventListener('click', initGame);
            
            // Help button
            document.getElementById('help-btn').addEventListener('click', () => {
                document.getElementById('instructions').style.display = 'block';
            });
            
            // Close help button
            document.getElementById('close-help').addEventListener('click', () => {
                document.getElementById('instructions').style.display = 'none';
            });
        });
    </script>
</body>
</html>
`
