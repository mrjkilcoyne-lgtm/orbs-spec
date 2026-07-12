# Flutter

## Scope
Flutter framework: widgets, state management, rendering, and cross-platform build systems for iOS, Android, Web, and Desktop.

## Core principles
- Flutter uses a widget tree; widgets are immutable and describe UI at a point in time; the framework rebuilds the tree when state changes and calculates diffs.
- StatefulWidget holds mutable state; setState() rebuilds the widget and its descendants — but only this widget's subtree, not the whole app.
- Provider (or Riverpod) manages state at scale: a ChangeNotifier or ValueNotifier notifies listeners, rebuilding only dependent widgets; complex state across features uses MultiProvider.
- Rendering is two-pass: layout (measure constraints down, return size up), then paint (draw order, clipping); expensive operations (shadows, blurs) have high cost.
- Hot reload restarts the Dart VM (not the app) and reruns the main function; state is preserved if it's in a static or global scope, but not if it's in widget state.

## Apex practices
- Use Riverpod over Provider for type safety and better code generation support; it scales better to complex state dependencies.
- Separate business logic from UI: create Services/ViewModels that Provider/Riverpod exposes, keeping widgets thin and testable.
- Profile with DevTools and frame rate monitor; jank (dropped frames) usually comes from synchronous work in build(); move heavy operations to compute-expensive tasks or background isolates.
- Test widgets with flutter test, Mockito, and golden tests (screenshot comparison); verify animations with WidgetTester.pump().

## Pitfalls
- setState() on a StatefulWidget is cheap, but calling it from a grandchild rebuilds ancestors unnecessarily — use Provider to lift state instead.
- Over-nesting widgets; each level of nesting adds to the tree traversal cost; flatten where possible using Widgets.
- GC pauses from large list views; use ListView.builder() (virtual scrolling), not ListView() with children; Riverpod's .select() to rebuild only affected widgets.

## Tools & references
Flutter documentation and codelabs, Dart language guide, flutter_test, Riverpod docs, Golden toolkit; "Flutter in Action" (Windmill); DevTools profiling.
