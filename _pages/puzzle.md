---
layout: page
permalink: /DoorPuzzle/
title: DooR Puzzle
nav: false
nav_order: 9
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>The Golem's Magnet Puzzle</title>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel+Decorative:wght@400;700&family=MedievalSharp&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'MedievalSharp', 'Cinzel Decorative', serif; 
            background-color: #1a1a1a;
            color: #f5f5dc; 
            display: flex;
            justify-content: center;
            align-items: flex-start; /* Align to top to allow scrolling if content is tall */
            min-height: 100vh; /* Full viewport height */
            margin: 0;
            padding: 20px;
            box-sizing: border-box; /* Include padding in element's total width and height */
            overflow-y: auto; /* Allow vertical scrolling */
        }

        .game-container {
            background-color: #2c2c2c; 
            border: 5px solidrgb(57, 23, 23); /* Darker stone/metal border */
            border-radius: 15px; /* Rounded corners for a crafted look */
            padding: 25px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.7); /* Deep shadow for depth */
            text-align: center;
            max-width: 600px; /* Max width for larger screens */
            width: 100%; /* Responsive width */
            margin-top: 20px; /* Space from top */
        }

        /* Headings */
        h1, h2 {
            color: #daa520; /* Goldenrod for a metallic/magical accent */
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5); /* Text shadow for depth */
            margin-bottom: 20px;
        }

        /* Puzzle Board Grid */
        .puzzle-board {
            display: grid;
            grid-template-columns: repeat(3, 1fr); /* 3 columns, equal width */
            grid-template-rows: repeat(3, 1fr); /* 3 rows, equal height */
            width: 300px; /* Base size for the puzzle board */
            height: 300px; /* Ensure it's a perfect square */
            margin: 0 auto 25px auto; /* Center board, add space below */
            border: 3px solid #6b6b6b; /* Lighter stone/metal border for the puzzle frame */
            border-radius: 8px; /* Slightly rounded corners for the board */
            overflow: hidden; /* Ensures tiles don't overflow rounded corners */
            box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.5); /* Inner shadow for depth */
            background-color: #3a3a3a; /* Background for the empty slot area */
        }

        /* Individual Puzzle Tile */
        .puzzle-tile {
            width: 100%; /* Fill grid cell */
            height: 100%; /* Fill grid cell */
            background-image: url('https://storage.googleapis.com/generative-ai-image-store/g_a_i_d_8_D2j7_1721469411931_300x300.png'); /* Generated image for the puzzle */
            background-size: 300% 300%; /* Scale background image to cover 3x3 grid */
            border: 1px solid #5a5a5a; /* Subtle border between tiles */
            box-sizing: border-box; /* Include border in tile size */
            cursor: pointer;
            transition: transform 0.2s ease-in-out, box-shadow 0.2s ease-in-out; /* Smooth movement and shadow transition */
            display: flex; /* For centering text if any */
            justify-content: center;
            align-items: center;
            font-size: 2em; /* For debugging tile numbers */
            color: rgba(255, 255, 255, 0.0); /* Hide numbers normally, set to 0.5 for debugging */
            border-radius: 5px; /* Slight rounding for tiles */
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3); /* Subtle tile shadow */
        }

        /* Hover effect for tiles */
        .puzzle-tile:not(.empty-tile):hover {
            transform: translateY(-3px); /* Lift effect */
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5); /* More prominent shadow */
        }

        /* Empty Slot Styling */
        .empty-tile {
            background-image: none; /* No image for the empty slot */
            background-color: #3a3a3a; /* Darker background for the empty slot */
            cursor: default;
            border: 1px dashed #6b6b6b; /* Dashed border for empty slot */
            box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.6); /* Inner shadow for empty slot */
        }

        /* Controls Area */
        .controls {
            margin-bottom: 25px;
            display: flex;
            justify-content: center;
            gap: 15px; /* Space between buttons */
            flex-wrap: wrap; /* Allow buttons to wrap on smaller screens */
        }

        /* Button Styling */
        button {
            background: linear-gradient(to bottom, #5a5a5a, #3a3a3a); /* Metallic gradient */
            color: #f5f5dc; /* Light text */
            border: 2px solid #daa520; /* Goldenrod border */
            border-radius: 8px; /* Rounded corners */
            padding: 12px 25px;
            font-size: 1.1em;
            font-family: 'Cinzel Decorative', serif; /* D&D font for buttons */
            cursor: pointer;
            transition: background-color 0.2s ease, transform 0.1s ease, box-shadow 0.2s ease;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4); /* Button shadow */
            text-transform: uppercase; /* Uppercase text */
            letter-spacing: 1px;
        }

        button:hover {
            background: linear-gradient(to bottom, #6b6b6b, #4a4a4a); /* Lighter gradient on hover */
            transform: translateY(-2px); /* Slight lift */
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.6); /* Enhanced shadow */
        }

        button:active {
            transform: translateY(0); /* Press effect */
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.4);
        }

        /* Message Box */
        .message-box {
            background-color: #3a3a3a; /* Darker background for messages */
            border: 2px solid #daa520; /* Goldenrod border */
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 25px;
            min-height: 40px; /* Ensure it has a minimum height */
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 1.2em;
            color: #f5f5dc;
            box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.4); /* Inner shadow */
        }

        /* Reference Image Container */
        .reference-image-container {
            margin-top: 30px;
            padding-top: 20px;
            border-top: 2px dashed #4a4a4a; /* Separator line */
            text-align: center;
        }

        .reference-image-container img {
            width: 250px; /* Slightly smaller than puzzle for reference */
            height: 250px;
            border: 3px solid #daa520; /* Goldenrod border */
            border-radius: 8px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.6); /* Shadow for the image */
            display: block; /* Remove extra space below image */
            margin: 0 auto; /* Center the image */
        }

        /* Responsive Adjustments */
        @media (max-width: 480px) {
            .game-container {
                padding: 15px;
                margin-top: 10px;
            }

            .puzzle-board {
                width: 280px; /* Smaller board on small screens */
                height: 280px;
            }

            h1 {
                font-size: 1.8em;
            }

            button {
                padding: 10px 20px;
                font-size: 1em;
            }

            .message-box {
                font-size: 1em;
            }

            .reference-image-container img {
                width: 200px;
                height: 200px;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>The Golem's Magnet Puzzle</h1>
        <div class="puzzle-board" id="puzzle-board">
            <!-- Puzzle tiles will be generated here by JavaScript -->
        </div>
        <div class="controls">
            <button id="shuffle-button">Shuffle</button>
            <button id="new-game-button">New Game</button>
        </div>
        <div class="message-box" id="message-box">Solve the Golem's Puzzle!</div>
        <div class="reference-image-container">
            <h2>Reference Image</h2>
            <!-- This is the generated D&D themed magnet image -->
            <img id="reference-image" src="https://oscarelliott.github.io/assets/img/" alt="D&D Golem Magnet Puzzle Image">
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const puzzleBoard = document.getElementById('puzzle-board');
            const shuffleButton = document.getElementById('shuffle-button');
            const newGameButton = document.getElementById('new-game-button');
            const messageBox = document.getElementById('message-box');
            const referenceImage = document.getElementById('reference-image');

            // Game state variables
            let puzzleState = []; // Represents the current order of tiles (0-8, 0 is empty)
            const solvedState = [1, 2, 3, 4, 5, 6, 7, 8, 0]; // The correct order
            const boardSize = 3; // 3x3 grid
            const totalTiles = boardSize * boardSize; // 9 tiles (8 pieces + 1 empty)
            const puzzleImageSrc = referenceImage.src; // Get image source from the reference image
            const tileWidth = 100; // Assuming 300x300 image, each tile is 100x100

            /**
             * Initializes the game by setting up event listeners and starting a new game.
             */
            function initGame() {
                shuffleButton.addEventListener('click', shufflePuzzle);
                newGameButton.addEventListener('click', newGame);
                newGame(); // Start a new game on load
            }

            /**
             * Starts a new game: resets the puzzle to solved, then shuffles it.
             */
            function newGame() {
                puzzleState = [...solvedState]; // Reset to solved
                messageBox.textContent = 'Solve the Golem\'s Puzzle!';
                shufflePuzzle(); // Shuffle for a new game
            }

            /**
             * Renders the current state of the puzzle to the DOM.
             * Creates or updates tile elements based on `puzzleState`.
             */
            function renderPuzzle() {
                puzzleBoard.innerHTML = ''; // Clear existing tiles

                for (let i = 0; i < totalTiles; i++) {
                    const tileValue = puzzleState[i]; // Get the original tile number (1-8 or 0 for empty)
                    const tileDiv = document.createElement('div');
                    tileDiv.classList.add('puzzle-tile');

                    if (tileValue === 0) {
                        tileDiv.classList.add('empty-tile');
                        tileDiv.dataset.value = '0'; // Store original value
                    } else {
                        // Calculate background position for the specific piece of the image
                        // (tileValue - 1) because tileValue is 1-8, but indices are 0-7
                        const originalIndex = tileValue - 1;
                        const col = originalIndex % boardSize;
                        const row = Math.floor(originalIndex / boardSize);

                        // Set background position to show the correct part of the image
                        tileDiv.style.backgroundImage = `url('${puzzleImageSrc}')`;
                        tileDiv.style.backgroundPosition = `-${col * tileWidth}px -${row * tileWidth}px`;
                        tileDiv.dataset.value = tileValue.toString(); // Store original value
                        tileDiv.addEventListener('click', handleTileClick);
                    }
                    puzzleBoard.appendChild(tileDiv);
                }
            }

            /**
             * Handles a click on a puzzle tile.
             * Checks if the tile can move and performs the swap if valid.
             * @param {Event} event - The click event.
             */
            function handleTileClick(event) {
                const clickedTileElement = event.target;
                const clickedTileValue = parseInt(clickedTileElement.dataset.value);

                // Find the index of the clicked tile in the current puzzleState
                const clickedTileCurrentIndex = puzzleState.indexOf(clickedTileValue);
                const emptyTileCurrentIndex = puzzleState.indexOf(0);

                // Check if the clicked tile is adjacent to the empty tile
                if (isAdjacent(clickedTileCurrentIndex, emptyTileCurrentIndex)) {
                    // Swap tiles in the puzzleState array
                    [puzzleState[clickedTileCurrentIndex], puzzleState[emptyTileCurrentIndex]] =
                    [puzzleState[emptyTileCurrentIndex], puzzleState[clickedTileCurrentIndex]];

                    renderPuzzle(); // Re-render the puzzle after swap

                    if (checkWin()) {
                        messageBox.textContent = 'Puzzle Solved! The Golem is pleased!';
                        // Optionally disable further moves or buttons
                        puzzleBoard.querySelectorAll('.puzzle-tile').forEach(tile => {
                            tile.removeEventListener('click', handleTileClick);
                            tile.style.cursor = 'default';
                        });
                    } else {
                        messageBox.textContent = 'Keep going, adventurer!';
                    }
                }
            }

            /**
             * Checks if two tile indices are adjacent on the board (horizontally or vertically).
             * @param {number} idx1 - First tile index.
             * @param {number} idx2 - Second tile index.
             * @returns {boolean} True if adjacent, false otherwise.
             */
            function isAdjacent(idx1, idx2) {
                const row1 = Math.floor(idx1 / boardSize);
                const col1 = idx1 % boardSize;
                const row2 = Math.floor(idx2 / boardSize);
                const col2 = idx2 % boardSize;

                // Check if in the same row and columns are one apart
                const sameRow = row1 === row2 && Math.abs(col1 - col2) === 1;
                // Check if in the same column and rows are one apart
                const sameCol = col1 === col2 && Math.abs(row1 - row2) === 1;

                return sameRow || sameCol;
            }

            /**
             * Checks if the current puzzle state matches the solved state.
             * @returns {boolean} True if solved, false otherwise.
             */
            function checkWin() {
                // Compare each element of puzzleState with solvedState
                for (let i = 0; i < totalTiles; i++) {
                    if (puzzleState[i] !== solvedState[i]) {
                        return false;
                    }
                }
                return true;
            }

            /**
             * Shuffles the puzzle tiles randomly, ensuring the puzzle is solvable.
             */
            function shufflePuzzle() {
                let shuffledArr;
                do {
                    shuffledArr = [...solvedState]; // Start with solved state
                    // Fisher-Yates shuffle algorithm
                    for (let i = shuffledArr.length - 1; i > 0; i--) {
                        const j = Math.floor(Math.random() * (i + 1));
                        [shuffledArr[i], shuffledArr[j]] = [shuffledArr[j], shuffledArr[i]];
                    }
                } while (!isSolvable(shuffledArr)); // Keep shuffling until solvable

                puzzleState = shuffledArr;
                renderPuzzle();
                messageBox.textContent = 'Puzzle shuffled! Good luck!';
            }

            /**
             * Checks if a given 8-puzzle configuration is solvable.
             * For an 8-puzzle, a configuration is solvable if the number of inversions is even.
             * An inversion is a pair of tiles (A, B) where A comes before B in the linear
             * representation, but A's value is greater than B's value. The empty space (0) doesn't count.
             * @param {Array<number>} arr - The puzzle state array.
             * @returns {boolean} True if solvable, false otherwise.
             */
            function isSolvable(arr) {
                let inversions = 0;
                const tempArr = arr.filter(tile => tile !== 0); // Exclude the empty tile

                for (let i = 0; i < tempArr.length - 1; i++) {
                    for (let j = i + 1; j < tempArr.length; j++) {
                        if (tempArr[i] > tempArr[j]) {
                            inversions++;
                        }
                    }
                }
                return inversions % 2 === 0; // Solvable if inversions count is even
            }

            initGame();
        });
    </script>
</body>
</html>
