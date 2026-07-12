# AR/VR Design

## Scope
Spatial design for immersive platforms: 3D composition, spatial audio, comfort (motion sickness prevention), and interaction paradigms specific to head-mounted and mixed-reality displays.

## Core principles
- VR is spatial, not 2D: composition, lighting, and perspective work differently in 360° with binocular vision; what reads flat on screen can be disorienting in VR.
- Comfort is non-negotiable: motion mismatch (visual motion without physical motion) causes sickness; fixed horizon lines, controlled camera movement, and stable frame rate (90 Hz minimum) are mandatory.
- Depth perception in VR: stereoscopic rendering creates convergence (eye crossing) cues; extreme depth (object very close or far) creates eye strain — stay in a comfortable range (0.5m to 20m).
- Interaction in AR/VR requires new metaphors (gaze-based, gesture, spatial menu systems) because mouse and keyboard don't exist; spatial UI scales to viewer distance and respects occlusion.
- Performance is stricter: 90 Hz in VR requires 11ms frame budget; miss frames and users feel sick; optimize aggressively.

## Apex practices
- Design for seated and standing users separately; standing users turn more, see further; seated users expect a more limited FOV.
- Use spatial audio (3D sound positioning) to guide attention and create immersion; sound from off-screen is powerful in VR.
- Test on the actual hardware early (Meta Quest, HTC Vive, PlayStation VR); editor simulations miss motion and presence cues.
- Implement comfortable locomotion: teleportation (snap turns) is comfortable, smooth movement with smooth turning can cause sickness; let users choose.

## Pitfalls
- Motion sickness from aggressive camera movement or mismatched visual-vestibular input (seeing motion without moving).
- Ignoring the limited tracking space; objects placed outside playable area cause frustration or safety risk.
- Assuming 2D UI scaling to 3D; reading small text at arm's length in VR is impossible; increase font size significantly.

## Tools & references
Unity (standard VR engine), Unreal Engine 5 (high-fidelity VR), Meta Horizon SDK, PlayStation VR SDK, Spatial design (Nielsen Norman Group VR research), latency and comfort (Oculus best practices).
