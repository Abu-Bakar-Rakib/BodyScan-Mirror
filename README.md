<div align="center">

# X-Ray Mirror

**See the anatomy beneath your reflection.**

A browser-based, real-time AR anatomy visualization that overlays interactive 3D anatomy on your webcam feed—powered by Three.js and MediaPipe.

[Launch the demo](xray.html#demo) · [Run with your camera](#quick-start) · [Privacy & safety](#privacy--safety)

</div>

---

## At a glance

| | |
| --- | --- |
| **Experience** | Real-time browser AR with face, body-pose, and hand tracking |
| **Anatomy** | Skull, brain, skeleton, organs, muscles, and hand bones |
| **Privacy** | Video is processed locally in your browser; frames are not uploaded |
| **Format** | Self-contained `xray.html` application |

## Highlights

### Head and face

- FaceLandmarker tracking for a detailed 3D cranium, articulated jaw, cerebrum, hindbrain, eyeballs, facial muscles, and head outline.
- Jaw movement follows the `jawOpen` blendshape.
- Automatic 2D-to-3D alignment, with **Fit to my head** controls for size, width, height, depth, and X/Y/Z offset. Adjustments are saved in `localStorage`.
- Pose-based head fallback when you move farther from the camera.

### Body and anatomy

- PoseLandmarker tracking drives an articulated skeleton, including the spine, ribcage, sternum, clavicles, scapulae, pelvis, and limb bones.
- Visualizes internal organs including the heart, lungs, trachea and bronchi, liver, stomach, kidneys, and intestines.
- Adds torso and limb muscle groups, a contoured body silhouette, and a dark veil.
- Supports both a seated, desk-facing view and a full-body standing view. When hips are out of frame, a proportional torso anchor is synthesized.

### Hands

- HandLandmarker tracks up to two hands and displays 3D palm, carpal, and phalanx meshes.

### Visualization controls

- **Presets and layers:** Skull, Full skeleton, Organs, Brain, Muscles, and Everything, with individual layer toggles.
- **Look modes:** glowing additive X-ray shading with a Fresnel rim glow, or lit Solid mode with brightness control.
- **Mixed reality and cutaways:** blend the live camera feed through the anatomy, adjust edge feathering, or use Left, Right, Top, and Bottom slices. An X-ray lens follows your movement.
- **Labels and telemetry:** show anatomical callouts, tracking landmarks, FPS, and pose statistics.

## Quick start

Webcam access and ES module loading require a secure context: `http://localhost` or `https://`. Start a local static server from the project directory:

```bash
python -m http.server 8000
```

Open the app in **Chrome** or **Edge**:

- **Live webcam:** <http://localhost:8000/xray.html>
- **No-camera demo:** <http://localhost:8000/xray.html#demo>

Optional URL flags: `?still` freezes the animation and `?dump` renders a flattened PNG preview.

> **First-load requirement:** An internet connection is needed to fetch Three.js, MediaPipe Tasks Vision, and the MediaPipe landmark models from their CDNs. The app processes webcam frames in your browser; video frames are not uploaded.

## Technology

- **3D rendering:** [Three.js](https://threejs.org/) 0.160.0, with custom GLSL shaders for X-ray, Solid, and Veil modes.
- **Tracking:** [MediaPipe Tasks Vision](https://developers.google.com/mediapipe/solutions/vision/pose_landmarker) 0.10.14, using FaceLandmarker, PoseLandmarker, and HandLandmarker.
- **Interface:** HTML5 Canvas for shading and HUD overlays.
- **Packaging:** A single `xray.html` file with embedded quantized head and hand mesh buffers and procedurally generated full-body geometry.

## Privacy & safety

Camera access is used for live tracking and visualization in your browser. Video frames are not uploaded to a server. External libraries and landmark models are downloaded from CDNs when the app loads; see the first-load requirement above.

**For educational visualization only.** The anatomy is an adult reference model scaled and aligned to tracked pose. It is not a scan of your body and is not a medical tool.

## Attribution

Head and hand 3D models are from [BodyParts3D](https://lifesciencedb.jp/bp3d/), © The Database Center for Life Science, licensed under [CC Attribution-Share Alike 2.1 Japan](https://creativecommons.org/licenses/by-sa/2.1/jp/).
