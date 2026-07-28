# Mobile Architecture

## Scope
Architectural patterns for mobile apps: MVVM, repository pattern, dependency injection, separation of concerns, and testability.

## Core principles
- MVVM (Model-View-ViewModel) separates UI (View) from business logic (ViewModel) — the ViewModel exposes reactive data (LiveData, StateFlow, ObservableObject), and Views observe changes.
- Repository pattern abstracts data sources (API, database, cache); the app requests data from Repository, which decides where to fetch it — enables swappable backends and testability.
- Dependency Injection (DI) passes dependencies to components (constructor, setter, or container) rather than having them create their own — enables mocking in tests and runtime flexibility.
- Layering (Presentation, Domain, Data) organizes code by concern; the Domain layer is platform-agnostic (Kotlin, Swift), the Data layer handles APIs/databases, Presentation is UI-specific.
- State management at scale requires consistency: redux-like single sources of truth, or event-driven with eventual consistency; implicit shared state in multiple ViewModels is a trap.

## Apex practices
- Use Hilt (Android) or Dagger, Swinject (iOS) for DI; constructor injection is testable and explicit.
- Repository returns Flow<T> or LiveData<T> to expose data reactively; use Room + Flow for local caching with transparent background sync.
- ViewModel lifetime: create at Fragment/Screen level, not Activity/App level; lifecycle-aware components ensure cleanup.
- Test ViewModels and Repositories with dependency mocks; UI tests (Espresso, UITest) are slow and brittle compared to unit tests.

## Pitfalls
- God ViewModels: a ViewModel managing UI state, business logic, and data fetching all at once — split into smaller concerns.
- Skipping the Repository layer and having multiple sources of truth (API cache, DB cache, memory) — forces complicated sync logic throughout.
- Over-engineering DI: simple apps don't need a full container; manual injection is often clearer.

## Tools & references
MVVM architectural pattern, Repository pattern, Hilt (Android) / Swinject (iOS), LiveData / Flow / StateFlow, testable architecture practices; Google's Architecture samples; "Clean Architecture" (Martin).
