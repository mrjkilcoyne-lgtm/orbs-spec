# Camera & Sensors

## Scope
Accessing device hardware: cameras, microphones, accelerometers, gyroscopes, and computer vision.

## Core principles
- Camera permissions are app-level (iOS) and runtime-requested (Android 6+) — request permission only when needed (on camera screen, not app launch).
- Camera output is raw pixel data; for photos, encode to JPEG; for video, encode to H.264/H.265 in real-time (using hardware encoder) to avoid memory explosion.
- Motion sensors (accelerometer, gyroscope) send data at 50–100 Hz; each frame has x/y/z values — accumulating raw data fills memory; use a ring buffer or downsample.
- Computer vision (face detection, QR code scanning, pose estimation) is compute-heavy; use specialized libraries (MLKit, TensorFlow Lite) for real-time performance.
- Microphone permissions are separate from camera; concurrent camera + mic use adds overhead (CPU, power).

## Apex practices
- Use AVCaptureSession (iOS) or CameraX (Android) for camera management; they handle threading, lifecycle, and permissions.
- Hardware video encoding: specify encoder (H.264, H.265) to use device codec; software encoding is too slow for real-time.
- Motion sensor data is noisy; apply low-pass filters (exponential moving average) to smooth jitter.
- Test on real devices; simulators don't accurately simulate camera, motion, or location.

## Pitfalls
- Holding camera session open when not in use; it keeps the GPU active and drains battery.
- Processing full-resolution camera frames on the main thread; extract a downsampled preview for ML, keep full resolution for photos.
- Requesting all permissions at startup; permission fatigue causes users to deny; request only when needed (permission-with-context).

## Tools & references
iOS AVFoundation, Android CameraX, MLKit (vision tasks), TensorFlow Lite for on-device ML, CoreMotion (iOS), SensorManager (Android); ARKit/ARCore for augmented reality.
