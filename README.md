# Tic-tac-tow
Play with your friends with this exciting game
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic Tac Toe - Game Dua Pemain</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #1a2a6c, #b21f1f, #fdbb2d);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
            padding: 30px;
            width: 100%;
            max-width: 500px;
            text-align: center;
            animation: fadeIn 0.8s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        h1 {
            color: #333;
            margin-bottom: 20px;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
        }

        .status {
            font-size: 1.5rem;
            margin-bottom: 20px;
            padding: 10px;
            border-radius: 10px;
            background-color: #f0f0f0;
            transition: all 0.3s ease;
        }

        .board {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-gap: 10px;
            margin: 20px auto;
            max-width: 300px;
        }

        .cell {
            background-color: #fff;
            border: none;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            aspect-ratio: 1/1;
            font-size: 2.5rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .cell:hover {
            transform: translateY(-5px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
            background-color: #f9f9f9;
        }

        .cell.x {
            color: #e74c3c;
            animation: popIn 0.3s ease-out;
        }

        .cell.o {
            color: #3498db;
            animation: popIn 0.3s ease-out;
        }

        @keyframes popIn {
            0% { transform: scale(0.8); opacity: 0; }
            70% { transform: scale(1.1); }
            100% { transform: scale(1); opacity: 1; }
        }

        .controls {
            margin-top: 20px;
        }

        button {
            background: linear-gradient(to right, #3498db, #2ecc71);
            border: none;
            border-radius: 50px;
            color: white;
            padding: 12px 25px;
            font-size: 1rem;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
            margin: 0 10px;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 0, 0, 0.3);
        }

        button:active {
            transform: translateY(1px);
        }

        .winning-cell {
            animation: pulse 1s infinite;
            background-color: #f1c40f;
        }

        @keyframes pulse {
            0% { background-color: #f1c40f; }
            50% { background-color: #f39c12; }
            100% { background-color: #f1c40f; }
        }

        .player-x {
            color: #e74c3c;
            font-weight: bold;
        }

        .player-o {
            color: #3498db;
            font-weight: bold;
        }

        .score-board {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        .score {
            font-size: 1.2rem;
        }

        .sound-control {
            margin-top: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .sound-toggle {
            background: #6c757d;
            width: 50px;
            height: 26px;
            border-radius: 13px;
            position: relative;
            cursor: pointer;
        }

        .sound-toggle.active {
            background: #28a745;
        }

        .sound-toggle::after {
            content: '';
            position: absolute;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background: white;
            top: 3px;
            left: 3px;
            transition: all 0.3s;
        }

        .sound-toggle.active::after {
            left: 27px;
        }

        .creator-credit {
            margin-top: 25px;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 10px;
            font-size: 1rem;
            color: white;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            animation: slideUp 0.5s ease-out;
        }

        .creator-name {
            font-weight: bold;
            color: #f1c40f;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.3);
            font-size: 1.1rem;
        }

        @keyframes slideUp {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @media (max-width: 480px) {
            .container {
                padding: 20px;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .cell {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Tic Tac Toe</h1>
        <div class="status" id="status">Giliran: <span class="player-x">Pemain X</span></div>
        
        <div class="score-board">
            <div class="score">X: <span id="scoreX">0</span></div>
            <div class="score">O: <span id="scoreO">0</span></div>
        </div>
        
        <div class="board" id="board">
            <!-- Sel-sel papan akan diisi oleh JavaScript -->
        </div>
        
        <div class="controls">
            <button id="reset">Mulai Ulang</button>
            <button id="newGame">Permainan Baru</button>
        </div>
        
        <div class="sound-control">
            <span>Suara:</span>
            <div class="sound-toggle active" id="soundToggle"></div>
        </div>

        <!-- Kredit Pembuat -->
        <div class="creator-credit">
            <p>Dibuat dengan ❤️ oleh <span class="creator-name">Efan Gagah</span></p>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // Elemen DOM
            const boardElement = document.getElementById('board');
            const statusElement = document.getElementById('status');
            const resetButton = document.getElementById('reset');
            const newGameButton = document.getElementById('newGame');
            const scoreXElement = document.getElementById('scoreX');
            const scoreOElement = document.getElementById('scoreO');
            const soundToggle = document.getElementById('soundToggle');
            
            // Variabel game
            let board = ['', '', '', '', '', '', '', '', ''];
            let currentPlayer = 'X';
            let gameActive = true;
            let scores = { X: 0, O: 0 };
            let soundEnabled = true;
            let audioContext = null;
            
            // Kombinasi pemenang
            const winningConditions = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // Baris
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // Kolom
                [0, 4, 8], [2, 4, 6]             // Diagonal
            ];
            
            // Inisialisasi Audio Context
            function initAudio() {
                if (!audioContext) {
                    audioContext = new (window.AudioContext || window.webkitAudioContext)();
                }
            }
            
            // Fungsi untuk memainkan suara
            function playSound(type) {
                if (!soundEnabled || !audioContext) return;
                
                try {
                    const oscillator = audioContext.createOscillator();
                    const gainNode = audioContext.createGain();
                    
                    oscillator.connect(gainNode);
                    gainNode.connect(audioContext.destination);
                    
                    // Setel jenis suara berdasarkan aksi
                    switch(type) {
                        case 'click':
                            oscillator.type = 'sine';
                            oscillator.frequency.setValueAtTime(523.25, audioContext.currentTime); // C5
                            gainNode.gain.setValueAtTime(0.1, audioContext.currentTime);
                            oscillator.start(audioContext.currentTime);
                            oscillator.stop(audioContext.currentTime + 0.1);
                            break;
                        case 'win':
                            oscillator.type = 'sine';
                            const now = audioContext.currentTime;
                            oscillator.frequency.setValueAtTime(659.25, now); // E5
                            gainNode.gain.setValueAtTime(0.2, now);
                            
                            oscillator.frequency.setValueAtTime(783.99, now + 0.2); // G5
                            oscillator.frequency.setValueAtTime(1046.50, now + 0.4); // C6
                            
                            oscillator.start(now);
                            oscillator.stop(now + 0.6);
                            break;
                        case 'draw':
                            oscillator.type = 'sawtooth';
                            const now2 = audioContext.currentTime;
                            oscillator.frequency.setValueAtTime(220, now2); // A3
                            gainNode.gain.setValueAtTime(0.1, now2);
                            
                            oscillator.frequency.setValueAtTime(196, now2 + 0.2); // G3
                            oscillator.frequency.setValueAtTime(174.61, now2 + 0.4); // F3
                            
                            oscillator.start(now2);
                            oscillator.stop(now2 + 0.6);
                            break;
                        case 'switch':
                            oscillator.type = 'triangle';
                            const now3 = audioContext.currentTime;
                            oscillator.frequency.setValueAtTime(392, now3); // G4
                            gainNode.gain.setValueAtTime(0.1, now3);
                            
                            oscillator.frequency.setValueAtTime(440, now3 + 0.1); // A4
                            
                            oscillator.start(now3);
                            oscillator.stop(now3 + 0.2);
                            break;
                        case 'reset':
                            oscillator.type = 'square';
                            const now4 = audioContext.currentTime;
                            oscillator.frequency.setValueAtTime(261.63, now4); // C4
                            gainNode.gain.setValueAtTime(0.15, now4);
                            
                            oscillator.frequency.setValueAtTime(329.63, now4 + 0.1); // E4
                            oscillator.frequency.setValueAtTime(392, now4 + 0.2); // G4
                            
                            oscillator.start(now4);
                            oscillator.stop(now4 + 0.3);
                            break;
                    }
                } catch (error) {
                    console.log('Error memainkan suara:', error);
                }
            }
            
            // Inisialisasi papan
            function initializeBoard() {
                boardElement.innerHTML = '';
                for (let i = 0; i < 9; i++) {
                    const cell = document.createElement('div');
                    cell.classList.add('cell');
                    cell.setAttribute('data-index', i);
                    cell.addEventListener('click', () => handleCellClick(i));
                    boardElement.appendChild(cell);
                }
            }
            
            // Handle klik sel
            function handleCellClick(index) {
                if (board[index] !== '' || !gameActive) return;
                
                // Inisialisasi audio pada klik pertama
                if (!audioContext) {
                    initAudio();
                }
                
                // Update board dan tampilan
                board[index] = currentPlayer;
                const cell = document.querySelector(`.cell[data-index="${index}"]`);
                cell.textContent = currentPlayer;
                cell.classList.add(currentPlayer.toLowerCase());
                
                // Mainkan suara klik
                playSound('click');
                
                // Cek hasil game
                checkResult();
            }
            
            // Cek hasil game
            function checkResult() {
                let roundWon = false;
                let winningCombo = [];
                
                for (let i = 0; i < winningConditions.length; i++) {
                    const [a, b, c] = winningConditions[i];
                    if (board[a] && board[a] === board[b] && board[a] === board[c]) {
                        roundWon = true;
                        winningCombo = [a, b, c];
                        break;
                    }
                }
                
                if (roundWon) {
                    // Ada pemenang
                    gameActive = false;
                    scores[currentPlayer]++;
                    updateScores();
                    
                    // Animasi sel pemenang
                    winningCombo.forEach(index => {
                        const cell = document.querySelector(`.cell[data-index="${index}"]`);
                        cell.classList.add('winning-cell');
                    });
                    
                    // Mainkan suara kemenangan dengan delay kecil
                    setTimeout(() => {
                        playSound('win');
                    }, 300);
                    
                    statusElement.innerHTML = `Pemenang: <span class="player-${currentPlayer.toLowerCase()}">Pemain ${currentPlayer}</span>`;
                    return;
                }
                
                // Cek seri
                if (!board.includes('')) {
                    gameActive = false;
                    statusElement.textContent = 'Permainan Seri!';
                    
                    // Mainkan suara seri dengan delay kecil
                    setTimeout(() => {
                        playSound('draw');
                    }, 300);
                    return;
                }
                
                // Ganti pemain
                currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                
                // Mainkan suara ganti pemain
                playSound('switch');
                
                updateStatus();
            }
            
            // Update status
            function updateStatus() {
                const playerClass = currentPlayer === 'X' ? 'player-x' : 'player-o';
                statusElement.innerHTML = `Giliran: <span class="${playerClass}">Pemain ${currentPlayer}</span>`;
            }
            
            // Update skor
            function updateScores() {
                scoreXElement.textContent = scores.X;
                scoreOElement.textContent = scores.O;
            }
            
            // Reset game (tetap pertahankan skor)
            function resetGame() {
                board = ['', '', '', '', '', '', '', '', ''];
                gameActive = true;
                currentPlayer = 'X';
                
                // Hapus kelas animasi pemenang
                document.querySelectorAll('.cell').forEach(cell => {
                    cell.classList.remove('winning-cell');
                });
                
                // Mainkan suara reset
                playSound('reset');
                
                initializeBoard();
                updateStatus();
            }
            
            // Game baru (reset semua)
            function newGame() {
                scores = { X: 0, O: 0 };
                updateScores();
                resetGame();
            }
            
            // Toggle suara
            soundToggle.addEventListener('click', () => {
                soundEnabled = !soundEnabled;
                soundToggle.classList.toggle('active', soundEnabled);
                
                // Mainkan suara test saat mengaktifkan
                if (soundEnabled && audioContext) {
                    playSound('click');
                }
            });
            
            // Event listeners
            resetButton.addEventListener('click', resetGame);
            newGameButton.addEventListener('click', newGame);
            
            // Inisialisasi awal
            initializeBoard();
            updateStatus();
            
            // Inisialisasi audio dengan interaksi pengguna
            document.addEventListener('click', function initAudioOnInteraction() {
                if (!audioContext) {
                    initAudio();
                    // Mainkan suara test
                    setTimeout(() => playSound('click'), 100);
                }
                document.removeEventListener('click', initAudioOnInteraction);
            });
        });
    </script>
</body>
</html>
