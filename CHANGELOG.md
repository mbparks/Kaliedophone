# Changelog

All notable changes to KALEIDOPHONE (Field Instrument 076). This project does not promise backwards compatibility between versions.

## v0.4.0 - Kinetoscope

Added a Backdrop Mix control and clip recording.

### Added

- **Backdrop Mix slider.** Sets how strongly the camera composites over the backdrop engine, from barely there to fully covering. Replaces the previously fixed blend. Persists locally.
- **Clip recording.** A Record button captures the live canvas to a video file using the browser's MediaRecorder and canvas capture. A pulsing indicator shows elapsed time. Recording auto-stops after a minute, and the clip downloads as WebM (or MP4 where that is the supported format). The recording captures whatever is on the canvas, including camera lenses and backdrops.
- New self-test: the recording plumbing is present and degrades without throwing when the browser lacks MediaRecorder or canvas capture.

### Changed

- Quick-start help now mentions recording.
- Version bumped to 0.4.0. Release name Kinetoscope.

### Notes

- Recorded clips are video only, with no audio.

## v0.3.0 - Coloriste

Added a fourth camera lens and a way to place a signal engine behind the camera.

### Added

- **Hand-Tint lens.** Maps the camera's brightness straight through the active palette, redrawing the world in the palette's colors like a hand-colored Melies frame. The signal drives contrast and tint depth. Computed on a downscaled buffer and upscaled for speed.
- **Backdrop control.** Places a signal engine behind any camera lens, so the camera composites over a live painting rather than filling the frame. Cycles through Off, Aurora, Bloom, Phosphor, Strata, and Cymatic. Persists locally.
- Blend-aware compositing in all four camera lenses: with a Backdrop set, the lens skips its clearing pass and draws the camera at blend opacity over the engine behind it.
- New self-tests: the Hand-Tint lens resolves and degrades gracefully, and every Backdrop option maps to a real signal engine.

### Changed

- Quick-start help now mentions Hand-Tint and Backdrop.
- Version bumped to 0.3.0. Release name Coloriste, after the studio that hand-colored Melies films.

## v0.2.0 - Camera Obscura

Added the device camera as a live source and three signal-driven camera lenses.

### Added

- **Camera source.** The Studio can now open the device camera. The feed stays on the device and is never uploaded or recorded. The camera never starts on its own.
- **Scrying Glass lens.** Folds the camera into a rotating kaleidoscope. Symmetry sets the wedge count. Zoom, spin, and hue-churn ride on signal energy.
- **Seance lens.** A chromatic ghost. Two hue-shifted copies of the frame separate further apart as the signal gets louder, over persistence trails.
- **Heat Mirage lens.** Slices the picture into horizontal bands and shifts each one sideways by the spectrum amplitude at that frequency, with a palette wash overlay.
- **Camera Lens panel** below the canvas: Enable Camera, Flip (front and back), and Mirror.
- Camera preferences (mirror, facing) persist locally.
- A gentle on-canvas prompt when a camera lens is selected before the camera is on.
- Two new self-tests: all eight engine keys resolve to a render method, and the camera lenses degrade without throwing when there is no feed.

### Changed

- The engine picker now groups engines under Signal and Camera headings.
- Quick-start help now describes the camera lenses.
- Version bumped to 0.2.0. Release name Camera Obscura.

### Notes

- Camera lenses need a secure context (HTTPS or localhost) and a browser with the canvas `filter` property.

## v0.1.0 - First Light

First release of KALEIDOPHONE as a distinct Field Instrument. The receiver lineage comes from SPECTRUM (Field Instrument 064); the instrument is reframed around generative art.

### Added

- **Signal Studio** as the primary page. Reads the live spectrum and raw IQ every frame.
- Five signal engines: Aurora Ribbons, Radial Bloom, Phosphor Storm, Woven Strata, Cymatic Plate.
- Six palettes: Aurora, Melies, Marbling, Orrery, Ember, Spectral.
- Studio controls: Intensity, Persistence, Flow, Symmetry, Freeze, Clear, Caption toggle.
- Capture PNG with an optional caption plate carrying frequency, mode, palette, engine, and UTC timestamp.
- Live context strip on the Studio with tuned frequency, mode, SNR, and an audio proxy button.

### Changed

- New identity as Field Instrument 076. New title, wordmark, and console banner.
- **Phantasmagoria aesthetic.** Retired the Signal Corps olive-drab look. Midnight indigo grounds, a hand-scattered starfield, jewel-tone accents in gold, aqua, and rose, soft starlit cards, and a gradient wordmark. Typography moved to Abril Fatface, Space Grotesk, and Space Mono.
- The old Dashboard was reframed as the Receiver, a supporting source rather than a co-equal page.
- All three themes (Night, Day, High Contrast) recolored to the new palette, with WCAG AA verified by the in-app self-test.

### Notes

- Single-file HTML, no build step, local-first. Runs on the Simulator with no hardware.
