# Personal Color Analysis

A single-file browser app that analyzes uploaded photos to classify your personal color season (Spring, Summer, Autumn, or Winter) based on skin tone undertone and depth.

## How it works

Upload one or more photos of your face. The app will:

1. **Detect faces** using [face-api.js](https://github.com/justadudewhohacks/face-api.js) (TinyFaceDetector) running entirely in the browser
2. **Sample skin tone** by averaging pixel colors within the detected face region
3. **Classify undertone** (warm/cool/neutral) from the green-minus-blue channel balance in the sampled RGB
4. **Classify depth** (light/medium/deep) using perceptual luminance (WCAG formula)
5. **Determine your season** from the undertone + depth combination:
   - Warm + Light → Spring
   - Warm + Medium/Deep → Autumn
   - Cool + Light → Summer
   - Cool + Medium/Deep → Winter
   - Neutral → depth-based tiebreaker

More photos give a more stable result by averaging across multiple samples.

## Features

- **Manual overrides** — adjust undertone, depth, or season directly if the auto-classification is off
- **Debug mode** — toggle bounding box overlay on thumbnails to see what the face detector found (red = full detection box, green = skin sampling region, yellow dashed = fallback center crop when no face is detected)
- Runs entirely in the browser — no server, no uploads, no data leaves your device

## Usage

Open `index.html` in any modern browser. No build step, no dependencies to install.

```
open index.html
```

Or serve it locally if you want to avoid browser restrictions on local file access:

```
npx serve .
# or
python3 -m http.server
```
