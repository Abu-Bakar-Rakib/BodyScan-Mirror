# X-Ray Mirror

A real-time, single-file browser AR **X-Ray Mirror** that overlays interactive 3D anatomy—skull, brain, full-body skeleton, internal organs, muscles, and hand bones—onto your live webcam feed.

Everything runs **100% locally in your browser** using Three.js and MediaPipe; video frames are never uploaded anywhere.

---

## Features

- **Head & Facial Tracking (`FaceLandmarker`)**
  - Detailed 3D cranium, articulated jaw (`jawOpen` blendshape tracking), cerebrum, hindbrain, eyeballs, facial muscles, and head outline.
  - Automatic 2D-to-3D projection alignment plus manual **Fit to my head** sliders (size, width, height, depth, X/Y/Z offset) saved in `localStorage`.
  - Automatic pose-based head fallback when stepping far back from the camera.

- **Full-Body & Upper-Body Tracking (`PoseLandmarker`)**
  - **Skeleton:** 18-vertebra articulated spine, 11-pair ribcage & sternum, clavicles, scapulae, pelvis, humeri, paired radius & ulna forearms, femurs, patellae, paired tibia & fibula shins, and feet.
  - **Internal Organs:** beating heart, breathing lungs with trachea/bronchi, liver, stomach, kidneys, and intestines.
  - **Muscles & Outline:** torso and limb muscle groups plus a contoured body silhouette and dark veil.
  - Works both **sitting at a desk** (synthesizes a proportional torso anchor when hips are out of frame) and in **full-body standing view**.

- **Hand Bone Tracking (`HandLandmarker`)**
  - Tracks up to two hands with 3D palm/carpal and phalanx meshes.

- **Interactive Visualization Controls**
  - **Presets & Layers:** `Skull`, `Full skeleton`, `Organs`, `Brain`, `Muscles`, `Everything`, plus individual toggles.
  - **Look Modes:** glowing additive **X-ray** shader (Fresnel rim glow) or lit **Solid** 3D mode with brightness control.
  - **Mixed Reality & Cutaways:** blend real camera feed (`Real me showing through`), adjust `Edge feather`, or slice anatomy (`Left`, `Right`, `Top`, `Bottom`, or an **X-ray lens** that follows your index fingertip or mouse pointer).
  - **Anatomical Labels & Telemetry:** toggle **Show labels** for non-overlapping callouts and **Show tracking data** for live landmark overlays and FPS/pose stats.

---

## Quick Start

Because webcam access (`getUserMedia`) and ES module loading require a secure context (`http://localhost` or `https://`), serve the directory with any local static server:

```bash
# Python 3
python -m http.server 8000
```

Then open in **Chrome** or **Edge**:

- **Live webcam mode:** `http://localhost:8000/xray.html`
- **No-camera demo mode:** `http://localhost:8000/xray.html#demo`
  - Optional query flags: `?still` (freeze animation), `?dump` (render flattened PNG preview).

> **Note:** An internet connection is required on first load to fetch Three.js (`0.160.0`), `@mediapipe/tasks-vision` (`0.10.14`), and the MediaPipe `.task` landmark models from CDN.

---

## Tech Stack

- **Rendering:** [Three.js](https://threejs.org/) (`0.160.0`) with custom GLSL vertex/fragment shaders (`X-ray`, `Solid`, and `Veil` modes) + HTML5 2D Canvas (`#shade` & `#hud`).
- **Tracking:** [MediaPipe Tasks Vision](https://developers.google.com/mediapipe/solutions/vision/pose_landmarker) (`0.10.14`) — `FaceLandmarker`, `PoseLandmarker` (`pose_landmarker_lite`), and `HandLandmarker` (WebGL GPU delegate with automatic CPU fallback).
- **Packaging:** Self-contained single file (`xray.html`) with embedded quantized head/hand mesh buffers and procedural full-body geometry.

---

## Disclaimer & Attribution

- **Educational visualization only:** The anatomy is an adult reference model scaled and aligned to your tracked pose. It is not a scan of your body and is **not a medical tool**.
- **Head & hand 3D models:** [BodyParts3D](https://lifesciencedb.jp/bp3d/), © The Database Center for Life Science, licensed under [CC Attribution-Share Alike 2.1 Japan](https://creativecommons.org/licenses/by-sa/2.1/jp/) (models simplified and re-aligned).
