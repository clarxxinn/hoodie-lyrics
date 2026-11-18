# Hoodie — Kinetic Lyric Video

This project displays lyrics in a code-editor style with syntax highlighting, a neon cursor, synchronized camera movement, glitch effects, and audio playback.

## Project structure

```text
lyrics-code-hoodie/
├── index.html
├── css/
│   └── style.css
├── js/
│   └── script.js
└── assets/
    ├── css3.png
    ├── html5.png
    ├── js.png
    ├── mp3.png
    └── hoodielyrics.mp3
```

## Run the project

1. Open the `lyrics-code-hoodie` folder in VS Code.
2. Open `index.html` in a browser, or use VS Code Live Server.
3. Click or tap once to allow the browser to start audio playback.

Keep the folder structure intact so the CSS, JavaScript, audio, and icon paths continue to work.

## Where to edit

- `index.html` — page structure and file references.
- `css/style.css` — styling, colors, typography, camera and line appearance, and glitch effects.
- `js/script.js` — lyric timeline, animation, audio sync, speed settings, and keyboard shortcuts.
- `assets/` — audio and tab icons.

## Keyboard controls

- `Space` — Play / Pause
- `R` — Restart
- `←` / `→` — Rewind / Skip 3 seconds
- `+` / `-` — Adjust playback speed
- `0` — Reset speed to 1.0x

## Audio setup

Set the MP3 file name in `js/script.js`:

```js
const AUDIO_FILE = 'assets/hoodielyrics.mp3';
```

To run the lyrics without audio, use an empty value:

```js
const AUDIO_FILE = '';
```

Browsers may block autoplay. Click the page once or press a key before pressing `R` if playback does not start automatically.

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

Set `AUTO_LOOP` to `false` to stop instead of looping.

## Line timing

The lyrics are stored in the `timeline` array in `js/script.js`. Each line contains a `speed`, `pause`, and `text` value:

```js
{
  speed: 0.80,
  pause: 0.50,
  text: 'hello.world( "example" ){ line: "two" };',
  zoom: false,
  zoomOut: false,
  glitch: false
},
```

- `speed` controls typing speed. Higher values type faster; lower values type more slowly.
- `pause` sets the idle time after typing finishes before the next line starts.
- `text` contains the lyric line.
- `glitch: true` enables the red glitch effect for that line.
- `zoom` and `zoomOut` are reserved and remain `false`.

The typing duration is calculated automatically:

```text
typing duration = character count × BASE_CHAR_TIME / speed
line duration   = typing duration + pause
```

For example, a 40-character line with `speed: 0.60` and `pause: 0.50` takes approximately:

```text
40 × 0.052 / 0.60 + 0.50 = 3.97 seconds
```

Timings accumulate from the top of the timeline. Changing one line shifts every line after it.

## Syntax colors

The highlighting is automatic:

- `// comments` are green.
- Text inside quotes is orange.
- Names before `(` are yellow.
- Regular words are light blue.
- Punctuation and brackets are gold or gray.

Add words to `CONTROL_KW` for keyword-style red coloring. Add words to `TYPE_KW` for blue type/coloring.

## Troubleshooting

- **No sound:** Confirm that the MP3 file name in `AUDIO_FILE` matches the file exactly.
- **Lyrics run before the audio:** The browser blocked autoplay. Refresh, click the page once, and press `R`.
- **Lyrics do not match the vocals:** Adjust each line's `speed` and `pause` values.
- **Broken tab icon:** Make sure `html5.png` is in the `assets` folder, or remove the icon `<img>` tag.

## Creator credits

Created by the original project author. If you use or modify this project, please retain the original credit and follow:

- TikTok: [@clarxxinn](https://www.tiktok.com/@clarxxinn)
- Github: [@clarxxinn](https://github.com/clarxxinn)