# iOS/SwiftUI

## Scope
SwiftUI framework for building iOS interfaces: views, state management, layout system, previews, and integration with UIKit/AppKit.

## Core principles
- SwiftUI uses declarative syntax where views are functions of state; the framework rebuilds views when state changes — efficient diffing limits rebuilds, but untracked mutations lead to stale UI.
- @State, @Binding, @ObservedObject, @EnvironmentObject create reactive dependencies; @State is value-type storage, @ObservedObject wraps reference types, and missing annotations cause views to not update.
- View identity matters: List/ForEach with .id() ensures correct animations and state association; without it, views can swap identity during scrolling.
- The view hierarchy is rebuilt on every state change; conditional views, if-else, are free (not re-evaluated), but the function must return a concrete View type — AnyView erases type but adds overhead.
- SafeArea, padding, and frame modifiers compose; order matters (apply padding before frame to pad inside, after to pad outside).

## Apex practices
- Use @StateObject for view-model initialization (not @ObservedObject) to ensure the object lives as long as the view and isn't recreated on re-render.
- Leverage Previews with #Preview and #PreviewLayout to iterate on UI without building; use .previewDevice() for multiple devices.
- Extract views into small structs to limit rebuild scope; a 200-line view re-renders the whole tree; split into 20-line components to re-render only affected parts.
- Use .onAppear() for one-time side effects (API calls); .task() for async work with cancellation; avoid side effects in the view function body.

## Pitfalls
- Excessive re-renders from @ObservedObject in a List; each item observes a published property, causing all items to rebuild — use @State + @Binding or item-level @StateObject instead.
- Modifying @State directly in closures without triggering redraw; SwiftUI's diffing is structure-based, so mutating arrays/dicts in-place may not trigger updates.
- Preview code diverging from app code (different view models, stubs); preview data should closely mirror production for accurate testing.

## Tools & references
Apple's SwiftUI tutorials and documentation, Xcode Previews, Instruments (Core Animation, Memory), SwiftUI by Example (Hacking with Swift); GitHub Copilot for view templates.
