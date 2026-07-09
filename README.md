# KALEIDOPHONE

**Field Instrument 076 &middot; A Signal-to-Light Instrument**

Green Shoe Garage &middot; [mbparks.com](https://mbparks.com)

KALEIDOPHONE turns invisible radio into light. It listens to the airwaves the way a receiver does, then paints with what it hears. The name is borrowed from Charles Wheatstone's 1827 instrument, which made vibration visible as looping figures of light. This one does the same with radio: a Melies optical parlor that draws with the spectrum, the raw IQ, and now your own camera.

The art is the point. Listening is still there, one page away, but the Studio is the heart of the instrument.

---

## The Studio

The Studio is the landing page. It reads the live signal every frame and hands it to one of nine engines. Five paint from the signal alone. Four warp the device camera with it.

### Signal engines

- **Aurora Ribbons** feeds the spectrum into rising, drifting curtains with painterly persistence.
- **Radial Bloom** wraps the bins into a rotating kaleidoscope. The Symmetry slider sets the mirror count.
- **Phosphor Storm** plots the raw I and Q as a glowing Lissajous cloud, the signal at its rawest.
- **Woven Strata** reimagines the waterfall as warped, hue-cycling marbled fabric.
- **Cymatic Plate** turns the loudest spectral peaks into a morphing interference field.

### Camera lenses

Each lens takes the live camera feed and lets the signal drive the distortion.

- **Scrying Glass** folds the camera into a rotating kaleidoscope. Symmetry sets the wedge count; zoom, spin, and hue-churn ride on signal energy.
- **Seance** is a chromatic ghost. Two hue-shifted copies drift apart, separating further as the signal gets louder, smeared over persistence trails.
- **Heat Mirage** slices the picture into horizontal bands and shifts each one sideways by the spectrum amplitude at that frequency, so the image writhes along the shape of the signal, with a palette wash on top.
- **Hand-Tint** maps the camera's brightness straight through the active palette, so the world is redrawn in the palette's colors like a hand-colored Melies frame. The signal drives the contrast and depth of the tint.

### Palettes

Six hand-tinted ramps: Aurora, Melies, Marbling, Orrery, Ember, and a full Spectral. Each palette is a gradient compiled into a 256-entry lookup table that every engine samples.

### Controls

- **Intensity** scales how hard the signal pushes the image.
- **Persistence** sets how long previous frames linger.
- **Flow** sets the animation speed.
- **Symmetry** sets mirror counts for the kaleidoscopic engines.
- **Freeze** holds the current frame. **Clear** wipes the canvas.
- **Caption** toggles the export plate.
- **Capture PNG** saves the current frame.
- **Record** captures a short clip of the canvas to a video file.

### Capture

Capture PNG exports the canvas. With Caption on, it stamps a small plate carrying the instrument name, the tuned frequency and mode, the palette, the engine, and a UTC timestamp, so each image is tied to the exact moment of radio that made it.

Record captures a short clip of the canvas to a video file. Press it to start, press again to stop, and the clip downloads. Recording stops on its own after a minute so the files stay small. The clip is video only, and it captures whatever is on the canvas, including camera lenses and backdrops.

---

## The Camera Lens panel

Below the canvas:

- **Enable Camera** starts and stops the device camera. Choosing a Camera lens will also offer to turn it on.
- **Flip** switches between the front and back cameras.
- **Mirror** flips the image horizontally. On by default for the front camera.
- **Backdrop** places a signal engine behind the camera lens, so instead of filling the frame the camera composites over a live painting. Cycle through Off, Aurora, Bloom, Phosphor, Strata, and Cymatic to stand in front of the one you want.
- **Backdrop Mix** sets how strongly the camera sits over the backdrop, from barely there to fully covering.

The camera feed never leaves the device. It is drawn straight to a canvas in the page and is never uploaded, recorded to disk, or sent anywhere. The camera never starts on its own. You turn it on, and stopping it releases the camera hardware immediately.

---

## The Receiver

The Receiver page carries the full radio inherited from the SPECTRUM lineage: tuning by keypad, bands, arrow keys, or by clicking the spectrum; AM, FM, SSB, and CW modes; AGC, AF gain, squelch, and volume; a waterfall and real-time spectrum; decoders; memory channels; an RF lab; and a journal. The art keeps painting whatever the receiver hears.

Sources:

- **Simulator** runs a rich synthetic spectrum with no hardware. This is the fastest way to see the Studio move.
- **IQ replay** plays back a recorded WAV capture.
- **RTL-SDR** connects live over WebUSB in a supporting browser.

---

## Themes and accessibility

Three themes ship: Night (the default), a hand-tinted Day, and a High Contrast mode. Every text and background pair is checked against WCAG AA by a self-test that runs inside the app, using the same contrast math the standard defines. High Contrast is the standard companion whenever multiple themes exist.

The layout is fluid, the side menu collapses, there is a mute control, a feedback path, and the running version is always shown on the plate.

---

## Running it

KALEIDOPHONE is a single HTML file. No build step, no server, no dependencies to install. Open it in a browser and it runs.

A few browser notes:

- The **camera lenses** need a secure context. Serve the file over HTTPS, or open it from `localhost`. Over plain `http://` the browser will refuse the camera.
- The camera lenses use the canvas `filter` property for their hue and saturation churn. Current versions of Chrome, Edge, Firefox, and Safari all support it.
- **Live RTL-SDR** capture uses WebUSB, which is available in Chrome and Edge over a secure context. Firefox and Safari can still use the Simulator and IQ replay.

State (engine, palette, control positions, camera preferences, receiver settings) is saved locally in the browser.

---

## Data and privacy

Everything runs on the device. The camera feed, the audio, and the signal are processed in the page and are not transmitted. Clearing the browser's site data resets saved settings.

---

## Development standards

KALEIDOPHONE follows the Field Instrument house rules:

- Local-first, single-file HTML, no build step.
- Night default, WCAG AA verified in every theme, High Contrast as standard.
- Fluid sizing, collapsible menus, a mute control, a feedback mechanism, and a visible version.
- A browser self-test harness that must pass before release, reachable from the System page.
- Per-release file snapshots, versioned filenames, and a changelog and blog post for every release.
- Rewrite over patch. No backwards-compatibility guarantee between versions unless requested.

Run the self-test from the System page before shipping. It covers palette lookups, the sampler, every engine key resolving to a render method, the camera plumbing, graceful behavior when a lens has no camera feed, and WCAG AA across all three themes.

---

## Known Limitations

- The camera lenses depend on the canvas `filter` property. A browser without it will still show the camera, but without the hue and saturation churn.
- `getUserMedia` requires a secure context. Opened over plain `http://`, the camera will not start.
- The **Flip** control assumes the device has more than one camera. On a single-camera desktop it may do nothing.
- Camera lenses at a large canvas size can be demanding on low-end mobile GPUs. If the frame rate drops, shrink the window or switch to a signal engine.
- Live RTL-SDR needs WebUSB, so live hardware capture is limited to Chrome and Edge. Other browsers use the Simulator or IQ replay.
- Settings persist in the browser via local storage. A portable settings export and import file is not yet wired into the Studio.
- Clip recording uses the browser's MediaRecorder and canvas capture, which most current browsers support. The output is WebM where available and MP4 on some browsers. Recording is video only, with no audio, and stops after a minute.
- The receiver's decoders and DSP are inherited and functional, but the focus of this instrument is the art. Expect the radio to be capable rather than exhaustive.
- No backwards compatibility is promised between versions.

---

## Roadmap

- A portable export and import for art settings.
- Optional audio in the recorded clip, taken from the receiver.
- A small gallery of recent captures and clips inside the Studio.

---

## Credits

Built by M.B. Parks (N1HNP) at Green Shoe Garage. Part of the Field Instruments series. The receiver lineage comes from SPECTRUM (Field Instrument 064). The name honors Charles Wheatstone's Kaleidophone of 1827.

Make. Hack. Learn. Share. Repeat.

---

## License

GPL-3.0
