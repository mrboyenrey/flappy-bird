# Flappy Bird

A browser-based Flappy Bird clone built with plain HTML, CSS, and the Canvas API. Everything lives in one file, so the project is easy to run, inspect, and extend.

## Play Online

Play the live version here:

https://mrboyenrey.github.io/flappy-bird/

## Project Layout

```text
Dev/flappy bird/
├── index.html
└── README.md
```

- `index.html`: page markup, styles, canvas, and all game logic
- `README.md`: usage notes and build walkthrough

## Getting Started

Open `index.html` in any modern browser. There is no install step, build pipeline, or package dependency.

If you want to run it from a local server instead of opening the file directly, either of these works:

```bash
python3 -m http.server
```

```bash
npx serve
```

Then open the local URL shown in the terminal.

## Controls

| Input | Action |
|---|---|
| `Space` | Flap |
| `Enter` | Flap |
| `ArrowUp` | Flap |
| `ArrowDown` | Flap |
| Mouse click | Flap |
| Touch / tap | Flap |

## How to Play

1. Open the game in a browser.
2. Press a control key, click, or tap to start.
3. Keep the bird in the air and pass through each pipe gap.
4. Avoid the pipes, the ground, and the top edge of the canvas.
5. Each cleared pipe pair adds `1` point.
6. When you crash, press a control again to restart.

## Step-by-Step: How This Project Was Made

This project can be recreated in a simple sequence.

1. Create the project folder and add an `index.html` file.
2. Add the base HTML structure with a `<canvas>` element inside `<body>`.
3. Write CSS to center the canvas on the page, give the page a dark background, and style the canvas with a border, rounded corners, and shadow.
4. In a `<script>` block, grab the canvas with `document.getElementById()` and get the 2D drawing context with `getContext('2d')`.
5. Define the gameplay constants such as gravity, flap strength, pipe width, pipe gap, pipe speed, and pipe spawn interval.
6. Create the main game state variables: `state`, `score`, `bestScore`, `pipes`, `lastPipeTime`, and `groundOffset`.
7. Build the `bird` object with its position, velocity, size, rotation, and a `reset()` method.
8. Add a `spawnPipe()` function that generates a random top pipe height and pushes a new pipe object into the `pipes` array.
9. Add the `flap()` function to handle first start, normal jumps, and restarting after death.
10. Add the `restart()` function to reset the bird, clear existing pipes, reset score, and return to the `playing` state.
11. Register input handlers for keyboard, mouse, and touch so the same flap action works on desktop and mobile.
12. Implement rectangle collision detection with `rectCollide()` and use it inside `checkCollisions()` for pipes, ground, and ceiling.
13. Build the drawing helpers for the visual layers: background, clouds, ground, pipes, bird, score, idle panel, and game-over overlay.
14. Create the main `gameLoop(timestamp)` function using `requestAnimationFrame()`.
15. Inside the loop, update physics only when the state is `playing`: gravity, bird position, pipe movement, scoring, pipe cleanup, and collision checks.
16. Draw the full scene every frame in a fixed order so the canvas layers look correct.
17. Start the animation loop with `requestAnimationFrame()` after initializing the starting timestamp.
18. Add a `README.md` documenting controls, mechanics, structure, and the exact build process.

## Implementation Notes

### Core Constants

These values control the game feel and difficulty:

```js
const GRAVITY = 0.5;
const FLAP_STRENGTH = -9;
const PIPE_WIDTH = 60;
const PIPE_GAP = 160;
const PIPE_SPEED = 2.8;
const PIPE_INTERVAL = 1600;
```

### Game States

| State | Description |
|---|---|
| `idle` | Waiting for the first player input |
| `playing` | Bird, pipes, score, and collisions are updating |
| `dead` | Game-over screen is visible and input restarts the run |

### Main Functions

| Function | Purpose |
|---|---|
| `spawnPipe()` | Creates a new pipe pair with a random opening |
| `flap()` | Starts the game, makes the bird jump, or restarts after death |
| `restart()` | Resets bird position, score, pipes, and timing |
| `rectCollide()` | Performs axis-aligned rectangle overlap tests |
| `checkCollisions()` | Detects hits with pipes, ground, or ceiling |
| `drawBackground()` | Paints the sky gradient and clouds |
| `drawGround()` | Draws the ground and scrolling tile marks |
| `drawPipe()` | Renders one pipe pair |
| `drawBird()` | Draws the bird sprite and rotation |
| `drawScore()` | Draws the current score |
| `drawOverlay()` | Draws the game-over panel |
| `drawIdleScreen()` | Draws the start screen |
| `gameLoop()` | Updates game logic and renders each frame |

## Game Mechanics

| Parameter | Value |
|---|---|
| Gravity | `0.5` px/frame² |
| Flap velocity | `-9` px/frame |
| Pipe width | `60` px |
| Pipe gap | `160` px |
| Pipe speed | `2.8` px/frame |
| Pipe interval | `1600` ms |
| Ground line | `canvas.height - 80` |

Collision detection uses a slightly smaller bird hitbox than the drawn sprite, which makes the game feel a bit less punishing.

## Browser Support

The project works in browsers that support:

- HTML5 Canvas
- `requestAnimationFrame`
- Modern JavaScript features used in the file such as `const`, `let`, template literals, and `Array.includes()`

## Customization Ideas

- Reduce `PIPE_GAP` to make the game harder.
- Increase `PIPE_SPEED` for a faster pace.
- Change canvas width and height to create a different play area.
- Persist `bestScore` in `localStorage` if you want it to survive a page refresh.
