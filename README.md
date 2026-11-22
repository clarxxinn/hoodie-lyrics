# Hoodie — Hey Violet Lyrics Coding

This project displays the lyrics of "Hoodie" by Hey Violet in a code-editor style with syntax highlighting, a glowing neon cursor, synchronized camera movement, glitch effects, and audio playback.

## Project structure

```text
hoodie-lyrics/
├── index.html
├── css/
│   └── hoodie.css
├── js/
│   └── hoodie.js
└── assets/
    ├── css3.png
    ├── hoodie.mp3
    ├── html5.png
    ├── js.png
    └── mp3.png
```

## Run the project

1. Open the `hoodie-lyrics` folder in VS Code.
2. Open `index.html` in a browser, or use VS Code Live Server.
3. Click or tap once if the browser blocks automatic audio playback.

Keep the folder structure intact so the CSS, JavaScript, audio, and icon paths continue to work.

## Where to edit

- `index.html` — page structure, file references, and editor-style tabs.
- `css/hoodie.css` — styling, syntax colors, typography, cursor, camera appearance, and glitch effects.
- `js/hoodie.js` — lyric timeline, typing animation, audio playback, camera movement, speed settings, and keyboard shortcuts.
- `assets/` — audio file and editor tab icons.

## Keyboard controls

- `Space` — Play / Pause
- `R` — Restart the experience
- `←` / `→` — Rewind / Skip 3 seconds
- `+` / `=` — Increase playback speed
- `-` / `_` — Decrease playback speed
- `0` — Reset playback speed to 1.0x

## Audio setup

The MP3 file is configured in `js/hoodie.js`:

```js
const AUDIO_FILE = 'assets/hoodie.mp3';
```

To run the lyrics without audio, use an empty value:

```js
const AUDIO_FILE = '';
```

The project attempts to start audio automatically. If the browser blocks autoplay, click or tap anywhere on the page or press a key to unlock audio playback.

## Speed and pause settings

The overall playback speed is controlled by:

```js
let MASTER_SPEED = 1.0;
```

The end-of-song black pause and looping behavior are controlled by:

```js
const BLACK_PAUSE_END = 3.5;
const AUTO_LOOP = true;
```

- `MASTER_SPEED` controls the overall playback speed.
- `BLACK_PAUSE_END` sets the black screen pause after the song ends, in seconds.
- `AUTO_LOOP` enables or disables automatic replay.

Set `AUTO_LOOP` to `false` to stop instead of automatically restarting.

## Line timing

The lyrics are stored in the `timeline` array in `js/hoodie.js`.

Each line contains `speed`, `pause`, and `text` values, along with optional visual effect settings:

```js
{
    speed: 0.82,
    pause: 0.72,
    text: 'it.makes( "me_think" ){ about: "you" };',
    zoom: false,
    zoomOut: false,
    glitch: false
},
```

- `speed` controls the typing speed. Higher values type faster; lower values type more slowly.
- `pause` sets the waiting time after a line finishes typing before the next line starts.
- `text` contains the lyric line displayed on screen.
- `glitch: true` enables the red glitch appearance for that line.
- `zoom` and `zoomOut` are reserved visual settings.

The typing duration is calculated automatically:

```text
typing duration = character count × BASE_CHAR_TIME / speed
line duration   = typing duration + pause
```

The base typing time is configured in `js/hoodie.js`:

```js
const START_DELAY = 0.05;
const BASE_CHAR_TIME = 0.052;
```

For example, a 40-character line with `speed: 0.60` and `pause: 0.50` takes approximately:

```text
40 × 0.052 / 0.60 + 0.50 = 3.97 seconds
```

Timings accumulate from the beginning of the timeline. Changing one line's speed or pause shifts the timing of every line after it.

## Syntax colors

The syntax highlighting is handled automatically in `js/hoodie.js` and styled in `css/hoodie.css`.

- Control keywords are coral red.
- Types and reserved keywords are blue.
- Function names are yellow.
- Variables are light cyan.
- Text inside quotes is orange.
- Numbers are light green.
- Comments are green.
- Punctuation is gray.
- Brackets are gold.

The keyword categories can be customized using:

- `CONTROL_KW` — words that receive control keyword coloring.
- `TYPE_KW` — words that receive type keyword coloring.

## Visual effects

The visual appearance is controlled by `css/hoodie.css` and `js/hoodie.js`.

- **Neon cursor** — a glowing pink block cursor follows the typing animation.
- **Camera movement** — smoothly follows the currently active lyric line.
- **Active line highlighting** — keeps the current line sharp and fully visible.
- **Word zoom** — emphasizes selected words during playback.
- **Glitch effect** — changes lyric colors to red and adds distortion.
- **Black curtain** — creates a black screen transition at the end of playback.
- **Speed badge** — displays the current playback speed when adjusted.

## Troubleshooting

- **No sound:** Check that `hoodie.mp3` exists inside the `assets` folder and that `AUDIO_FILE` points to the correct path.
- **Audio does not autoplay:** Click or tap the page once to allow the browser to start playback.
- **Lyrics do not match the vocals:** Adjust the `speed` and `pause` values in the `timeline` array.
- **Lyrics type too fast or too slowly:** Adjust `BASE_CHAR_TIME` or individual line speeds.
- **Broken tab icons:** Make sure all four image files are inside the `assets` folder.
- **Project does not load correctly:** Check that the CSS and JavaScript file paths in `index.html` match the actual folder structure.

## Creator credits

Created by the original project author.

If you use or modify this project, please retain the original credit and respect the rights of the song, recording, and lyrics belonging to their respective owners.