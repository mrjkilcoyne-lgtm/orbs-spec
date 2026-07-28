# React Native

## Scope
React Native framework: bridge architecture, native modules, platform-specific code, and performance bottlenecks.

## Core principles
- React Native bridges JS (V8 or JSC) to native (iOS/Android); the bridge serializes data (JSON), crosses threads, and is a throughput bottleneck — high-frequency events (>60/sec) should stay native.
- Native modules implement platform-specific APIs; the bridge queues calls and executes them asynchronously, so JS doesn't block rendering — but callbacks block the native thread until they return.
- The JS thread runs React and user code; the native thread runs UI; the bridge synchronizes, so long JS tasks stall rendering and vice versa.
- Platform-specific code uses Platform.OS and conditional requires (.ios.js, .android.js); over-abstracting leads to lowest-common-denominator UX.
- FlatList virtualizes long lists; it measures and caches item heights, only rendering visible items — a huge performance win vs ScrollView for 1000+ items.

## Apex practices
- Profile with React DevTools (JS) and native profilers (Xcode Instruments, Android Profiler) in parallel — network + navigation time vs rendering time vs bridge latency are distinct.
- Use JSI (JavaScript Interface) for performance-critical native code (animations, video, audio) — it's faster than the bridge and allows direct access to JS objects.
- Optimize bundle size with code splitting and lazy loading; react-native-code-push for OTA updates without App Store review.
- Measure frame rate with Performance.now() and log 60 FPS targets; use react-native-performance-monitor to catch frame drops.

## Pitfalls
- Passing large objects over the bridge frequently (e.g., image data every frame) — serialize only necessary fields and batch updates.
- Ignoring GC pauses: JS GC can freeze rendering for 100+ ms; use memory profiler to detect leaks and over-allocations.
- Assuming iOS and Android performance are identical; they have different thread schedulers, GC, and native perf characteristics.

## Tools & references
React Native documentation, React DevTools, Xcode Instruments, Android Profiler, react-native-performance, react-native-debugger; "React Native in Action" (Kuhn et al.).
