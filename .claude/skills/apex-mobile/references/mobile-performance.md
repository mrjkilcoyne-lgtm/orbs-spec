# Mobile Performance

## Scope
Optimizing mobile app speed: startup time, memory, battery, frame rate, and profiling tools.

## Core principles
- Startup time (cold launch to interactive) is the first impression; >2 seconds loses users — profile with Xcode Time Profiler (iOS) or Android Profiler to find bottlenecks.
- Memory constraints on mobile (2–8 GB) are tighter than desktop; background processes and large bitmaps trigger OOMKiller — profile heap and monitor allocation peaks.
- Battery is precious; location, Bluetooth, motion sensors, and high CPU drain quickly — disable when not needed and batch operations.
- Frame rate (60 FPS on standard displays, 120 FPS on high refresh) depends on rendering latency; jank (dropped frames) comes from long frames (>16 ms at 60 FPS, >8 ms at 120 FPS).
- Network overhead: DNS + TLS handshake can add 100+ ms per connection — reuse connections and pipeline requests with HTTP/2.

## Apex practices
- Lazy load screens (don't create all UI upfront); defer decoding images and initializing expensive services until needed.
- Profile with native tools: Xcode Instruments (iOS), Android Profiler (Android); focus on longest frames and memory peaks.
- Use vector graphics (SVG, PDF) where possible instead of raster images — smaller, scalable, faster to render.
- Implement memory warnings: on iOS, implement didReceiveMemoryWarning; on Android, ComponentCallbacks.onTrimMemory — release caches early.

## Pitfalls
- Main/UI thread blocking on I/O, JSON parsing, or heavy computation — move to background thread (GCD, Coroutines).
- Image decoding on the main thread; decode in background and display cached bitmap to avoid frame jank.
- Ignoring app launch time; optimizing app open by 500 ms improves retention by 5–10%.

## Tools & references
Xcode Instruments (Core Animation, Memory, System Trace), Android Profiler, Systrace, Firebase Performance Monitoring; "High Performance iOS Apps" (Neuburg); Baseline profiling with Macrobenchmark.
