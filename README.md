
# Coin Flip

A web-based coin flip application that displays a 3D coin animation using Three.js, styled with Tailwind CSS. Users can click a button to flip a coin, view the result ("Heads" or "Tails"), and experience audio and haptic feedback. The app is responsive, accessible, and visually engaging, with a dark-themed interface inspired by a dice roller design.

## Features
- **3D Coin Animation**: Renders a 3D coin model (OBJ format) with realistic textures and animations using Three.js.
- **Interactive Flip**: Click the "Flip" button to trigger a coin flip animation, displaying "Heads" or "Tails" based on a random outcome.
- **Tailwind CSS Styling**: Clean, responsive UI with a dark background, modern typography (Space Grotesk and Noto Sans), and a centered layout.
- **Audio Feedback**: Plays a button click sound and a coin flip sound (currently using a placeholder dice roll sound).
- **Haptic Feedback**: Triggers device vibration on supported devices for a tactile experience.
- **Accessibility**: Includes `aria-live` for screen reader support to announce flip results.
- **Responsive Design**: Adapts to various screen sizes, with a fixed 300x300px canvas for the coin animation.

## Demo
[Insert link to live demo if hosted, e.g., on GitHub Pages or a web server]

## Prerequisites
- A modern web browser (e.g., Chrome, Firefox, Safari, Edge) with JavaScript enabled.
- Internet access for loading external dependencies (Tailwind CSS, Three.js, Google Fonts, and audio files) unless hosted locally.
- Optional: A device supporting the Vibration API for haptic feedback.

## Setup
1. **Clone or Download**:
   - Clone the repository or download the `index.html` file and associated assets (OBJ model and textures, if hosted locally).
   ```bash
   git clone <repository-url>
   ```

2. **File Structure**:
   Ensure the following files are available if hosting locally:
   - `index.html`: Main HTML file with the app's structure and logic.
   - `T_Quarter_AO.jpg`: Ambient occlusion texture for the coin.
   - `T_Quarter_Normal.jpg`: Normal map texture for the coin.
   - `00306_Quarter_SKFB.obj`: 3D coin model in OBJ format.
   - Audio files (optional, if hosted locally):
     - `mixkit-dice-rolling-777.mp3`: Placeholder sound for coin flip.
     - `mixkit-modern-click-1118.mp3`: Button click sound.

   If using external resources, ensure internet access to load:
   - Tailwind CSS: `https://cdn.tailwindcss.com`
   - Google Fonts: `https://fonts.googleapis.com`
   - Three.js and modules: `https://unpkg.com/three@0.160.0`
   - Audio files: `https://assets.mixkit.co`

3. **Local Hosting** (Optional):
   - Use a local server to serve the files (e.g., `http-server`, Python's `http.server`, or VS Code's Live Server) to avoid CORS issues with local file loading.
   ```bash
   python -m http.server 8000
   ```
   - Access the app at `http://localhost:8000`.

4. **Update Asset Paths** (if hosting locally):
   - Modify the paths in `textureLoader.load` and `loader.load` in the `<script>` section of `index.html` to point to local copies of `T_Quarter_AO.jpg`, `T_Quarter_Normal.jpg`, and `00306_Quarter_SKFB.obj`.
   - Update audio file paths in `<audio>` tags if hosting locally.

## Usage
1. Open the `index.html` file in a web browser (via a local server or hosted URL).
2. Click the "Flip" button to trigger the coin flip animation.
3. Watch the 3D coin spin and settle, displaying "Result: Heads" or "Result: Tails" in the UI.
4. Listen for a button click sound and a coin flip sound (placeholder dice roll sound).
5. Feel a vibration on supported devices during the flip.
6. Repeat by clicking the "Flip" button again (disabled during animation to prevent multiple flips).

## Customization
- **Coin Size**:
  - Adjust the `scaleFactor` in the OBJ loading section (e.g., `const scaleFactor = 3 / size`) to make the coin larger or smaller.
  - Modify the camera position (e.g., `camera.position.set(0, 0, 4)`) to zoom in (`z = 3`) or out (`z = 5`).
- **Audio**:
  - Replace the `coinFlipSound` source (`mixkit-dice-rolling-777.mp3`) with a more realistic coin clink sound. Update the `<audio id="coinFlipSound">` `src` attribute.
  - Adjust audio volumes in the script (e.g., `coinFlipSound.volume = 0.5`).
- **Model and Textures**:
  - Swap the OBJ model or textures by updating the paths in `loader.load` and `textureLoader.load`.
  - Ensure the new model's "Heads" side aligns with the negative Z-axis (`coinNormal = new THREE.Vector3(0, 0, -1)`), or adjust `coinNormal` in the `flipCoin` function.
- **Styling**:
  - Modify Tailwind classes in the HTML or CSS in the `<style>` section (e.g., change `.bg-coin` background color or `.coin-canvas` dimensions).
- **Accessibility**:
  - Add a hidden `<span class="sr-only">Flipping coin...</span>` during the flip animation to announce the action to screen readers.

## Troubleshooting
- **Coin Too Small/Large**:
  - Adjust `scaleFactor` (e.g., `2.5 / size` for smaller, `3.5 / size` for larger) or camera `z` position in the script.
- **Heads/Tails Incorrect**:
  - Verify the OBJ model's orientation in a 3D editor (e.g., Blender). If "Heads" is not on the negative Z-axis, update `coinNormal` in the `flipCoin` function (e.g., `new THREE.Vector3(0, 0, 1)` for positive Z).
  - Alternatively, invert the result logic: change `coinResult.textContent = `Result: ${isHeads ? 'Heads' : 'Tails'}` to `Result: ${isHeads ? 'Tails' : 'Heads'}`.
- **Model/Texture Fails to Load**:
  - Check console logs for errors. Ensure the OBJ and texture files are accessible or hosted correctly.
  - A red cube appears as a fallback if the OBJ fails to load.
- **Audio Not Playing**:
  - Ensure internet access for Mixkit audio files or host them locally.
  - Check browser permissions for audio playback (some browsers block autoplay without user interaction).
- **Vibration Not Working**:
  - Verify device/browser support for the Vibration API (e.g., supported on most mobile browsers but not all desktops).

## Technical Details
- **Dependencies**:
  - Tailwind CSS (CDN): For responsive styling.
  - Google Fonts: Space Grotesk and Noto Sans for typography.
  - Three.js (v0.160.0): For 3D rendering, including `OrbitControls` and `OBJLoader`.
  - Mixkit: Audio files for button click and coin flip (placeholder).
- **Canvas**:
  - Size: 300x300px (`max-width: 300px`, `height: 300px`).
  - Renderer: WebGL with antialiasing and shadow mapping.
- **Animation**:
  - Coin flips with random spin speeds, settling to show Heads or Tails using quaternion-based rotation.
  - Duration: 1.5s flip + 0.5s settle.
- **Accessibility**:
  - `aria-live="polite"` on the result div for screen reader announcements.
- **Browser Compatibility**:
  - Tested on modern browsers (Chrome, Firefox, Safari, Edge).
  - Requires WebGL support for 3D rendering.

## Future Improvements
- Add a loading spinner (e.g., Tailwind `animate-spin`) during OBJ/texture loading.
- Replace the placeholder coin flip sound with a metallic clink for realism.
- Enhance accessibility with additional screen reader announcements (e.g., "Flipping coin...").
- Allow users to rotate the coin manually using OrbitControls (currently disabled).
- Support multiple coin flips or a history of results.
- Optimize OBJ model loading for faster performance (e.g., use a lower-polygon model).

## License
[Insert license, e.g., MIT License]
```
MIT License

Copyright (c) 2025 [Your Name or Organization]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## Contributing
Contributions are welcome! Please submit a pull request or open an issue on the repository for bug reports, feature requests, or improvements.

## Contact
For questions or feedback, contact [Your Name or Email] or open an issue on the repository.

---

### Notes for Customization
- **File Naming**: Save this as `README.md` in your project directory.
- **Live Demo**: If you host the app (e.g., on GitHub Pages), add the URL to the "Demo" section.
- **License**: Replace `[Your Name or Organization]` in the MIT License with your details, or choose a different license.
- **Assets**: If you host the OBJ, textures, or audio files locally, update the README to reflect the local paths and setup instructions.
- **Improvements**: If you implement any suggested improvements (e.g., loading spinner, new audio), update the "Features" and "Future Improvements" sections.

If you need help with hosting, adding a specific feature (e.g., loading spinner), or modifying the README (e.g., adding a demo link or specific license), let me know! You can also provide details about your project setup (e.g., local vs. hosted assets) for more tailored instructions.
