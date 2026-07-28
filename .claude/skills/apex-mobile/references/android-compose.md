# Android Compose

## Scope
Jetpack Compose framework for Android UI: composables, recomposition, state management, theming, and interop with existing Views.

## Core principles
- Composables are functions that describe UI; recomposition reruns the function when state changes — but the framework skips functions whose inputs didn't change (smart recomposition).
- State in Compose uses mutableStateOf(), remember {}, and rememberSaveable{}; remember {} survives recomposition but not process death, rememberSaveable {} persists across recreation.
- Composition scope matters: state defined in a parent composable survives children's recomposition; state defined locally to a composable is lost on parent recomposition.
- Modifiers chain left-to-right and order matters: Modifier.size().padding() sizes first then pads; .padding().size() pads first then sizes the result.
- LazyColumn/LazyRow virtualize rendering (only visible items render), critical for scrolling performance — but state in each item must be explicit (@State, rememberSaveable).

## Apex practices
- Use ViewModels with compose-compatible architecture: store mutable state in ViewModel using StateFlow or LiveData, collect in composables with collectAsStateWithLifecycle().
- Decompose large composables into smaller ones; a 500-line composable recomposes as a unit; split it into 50-line components so only affected parts recompose.
- Preview composables with @Preview and @PreviewParameter to test multiple states without running the app; combine with Theme previews for dark mode.
- Use derivedStateOf {} to compute values during recomposition (e.g., list.size > 0) without new mutableState; it avoids creating new state objects.

## Pitfalls
- State hoisting gone wrong: lifting state too high causes entire screens to recompose on minor input changes; lift state only as high as needed.
- Misusing remember {}: objects recreated on recomposition (e.g., remember { mutableListOf() }) still get a fresh list; use rememberSaveable to persist state.
- Ignoring recomposition frequency: Compose logs skipped recompositions; high-frequency recompose can cause jank — measure with Compose performance tools.

## Tools & references
Google's Compose documentation and codelab, Jetpack Compose API, Android Studio's Compose Preview, Compose compiler metrics, Macrobenchmark for perf testing; "Now in Android" sample.
