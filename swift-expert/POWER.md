---
name: swift6-expert
displayName: Swift 6 Expert
description: Expert guidance on Swift 6 development including modern language features, API design, concurrency patterns, and best practices for iOS, macOS, watchOS, and visionOS
keywords: [swift, swift6, ios, macos, watchos, visionos, ipados, concurrency, async, await, actor, sendable, api-design, migration, swiftui, testing, core-data]
version: 1.0.0
---

# Swift 6 Expert

Expert guidance on Swift 6 development. This power provides comprehensive support for modern Swift programming, including language features, API design guidelines, concurrency patterns, framework integration, and migration strategies.

## Onboarding

### Required Extension

This power requires the Swift language extension for optimal functionality. The extension provides:
- Swift syntax highlighting and IntelliSense
- Code completion and navigation
- Build task integration
- Debugging support

**Installation Steps:**

1. Open the Extensions view in Kiro (Ctrl/Cmd+Shift+X)
2. Search for "Swift" by Swift Server Work Group
3. Click Install on the official Swift extension
4. Reload Kiro when prompted

**Alternative:** Install directly from [Open VSX Registry](https://open-vsx.org/extension/swiftlang/swift-vscode)

**Verification:**

After installation, open a `.swift` file and verify:
- Syntax highlighting is active
- Code completion works (type a few characters and press Ctrl+Space)
- You can navigate to definitions (Cmd/Ctrl+Click on symbols)

If you encounter issues, ensure you have:
- Xcode installed (macOS) or Swift toolchain installed (Linux)
- Swift command-line tools accessible in your PATH
- Workspace opened with Swift files

## When to Use This Power

Activate this power when working with:

- Swift 6 language features and migration
- API design following Swift conventions
- Modern concurrency (async/await, actors, tasks)
- SwiftUI and UIKit development
- Testing with Swift Testing framework
- Core Data and persistence
- iOS, iPadOS, macOS, watchOS, or visionOS development
- Code architecture and design patterns
- Performance optimization
- Strict concurrency checking and data race safety

## Getting Started

### Prerequisites

- Xcode 13+ (Xcode 15+ recommended for Swift 6 features)
- Swift 5.5+ (Swift 6+ for latest features)
- Target platform: iOS, iPadOS, macOS, watchOS, or visionOS

### Quick Start for Swift 6

1. **Follow Swift API Design Guidelines**: Write clear, idiomatic Swift code
   - Use descriptive names that read as grammatical English
   - Prefer clarity over brevity
   - Document public APIs

2. **Adopt Modern Language Features**:
   - Use Swift 6 language mode for new projects
   - Enable strict concurrency checking for data race safety
   - Leverage async/await for asynchronous operations

3. **Platform-Specific Development**:
   - Use SwiftUI for modern UI development
   - Integrate with platform frameworks (UIKit, AppKit, Core Data)
   - Follow platform conventions and best practices

## Core Concepts

### Swift API Design

Write clear, idiomatic APIs following Swift conventions:

```swift
// Good: Clear, grammatical usage
employees.remove(at: index)
x.insert(y, at: z)
x.subviews(havingColor: .blue)

// Bad: Unclear or redundant
employees.remove(index)
x.insertElement(y, position: z)
x.subviewsWithColor(.blue)
```

**Key principles**:
- Clarity at the point of use is paramount
- Include all words needed to avoid ambiguity
- Omit needless words
- Name based on roles, not types

### Modern Concurrency

Transform asynchronous code with Swift's structured concurrency:

```swift
// Before: Completion handlers
func fetchUser(completion: @escaping (Result<User, Error>) -> Void) {
    // ...
}

// After: Async/await
func fetchUser() async throws -> User {
    // ...
}
```

**Protect shared state with actors**:

```swift
actor DataCache {
    private var cache: [String: Data] = [:]
    
    func get(_ key: String) -> Data? {
        cache[key]
    }
    
    func set(_ key: String, value: Data) {
        cache[key] = value
    }
}
```

### Structured Concurrency

Manage asynchronous work safely:

```swift
// Parallel execution
async let users = fetchUsers()
async let posts = fetchPosts()
let (u, p) = try await (users, posts)

// Task groups for dynamic parallelism
await withTaskGroup(of: Result.self) { group in
    for item in items {
        group.addTask { await process(item) }
    }
}
```

### Type Safety

Mark types as safe for concurrent access:

```swift
struct UserProfile: Sendable {
    let id: UUID
    let name: String
}
```

## Agent Behavior Guidelines

When providing Swift 6 development guidance, follow these rules:

### 1. Follow Swift Conventions

Always adhere to Swift API Design Guidelines:
- Write code that reads as grammatical English
- Prioritize clarity at the point of use
- Use proper naming conventions (UpperCamelCase for types, lowerCamelCase for everything else)
- Document public APIs with clear, concise comments

### 2. Prefer Apple Frameworks

Favor Apple programming languages and frameworks:
- Prefer Swift over alternatives
- Use platform-native APIs (SwiftUI, UIKit, AppKit, Core Data)
- Reference platforms by official names (iOS, iPadOS, macOS, watchOS, visionOS)
- Avoid suggesting iOS-only APIs for macOS projects

### 3. Use Modern Swift Testing

When writing tests, prefer Swift Testing framework over XCTest:

```swift
import Testing

@Suite("User Profile Tests")
struct UserProfileTests {
    @Test("Creating a valid profile")
    func createValidProfile() async throws {
        let profile = UserProfile(name: "Alice")
        #expect(profile.name == "Alice")
    }
}
```

### 4. Analyze Project Settings (For Concurrency)

Before proposing concurrency-related fixes, check:
- Swift language mode (Swift 5.x vs Swift 6)
- Strict concurrency checking level (minimal/targeted/complete)
- Default actor isolation settings
- Enabled upcoming features

**Where to check**:
- SwiftPM: `Package.swift` for tools version, features, and settings
- Xcode: `project.pbxproj` for `SWIFT_VERSION`, `SWIFT_STRICT_CONCURRENCY`, `SWIFT_DEFAULT_ACTOR_ISOLATION`

### 5. Identify Isolation Boundaries (For Concurrency)

Before proposing concurrency fixes, determine:
- Is this `@MainActor` isolated?
- Is this a custom actor?
- Is this nonisolated?
- What isolation does the caller have?

### 6. Don't Default to @MainActor

Don't recommend `@MainActor` as a blanket fix. Justify why main-actor isolation is correct:
- Is this UI-related code?
- Does it need to update SwiftUI views?
- Would a custom actor be more appropriate?

### 7. Prefer Structured Concurrency

Recommend structured concurrency (child tasks, task groups) over unstructured tasks. Only suggest `Task.detached` with clear justification.

### 8. Require Safety Documentation

When recommending escape hatches, require:
- `@preconcurrency`: Document why needed and when to revisit
- `@unchecked Sendable`: Document safety invariant
- `nonisolated(unsafe)`: Document thread-safety guarantee
- Create follow-up ticket to remove or migrate

### 9. Optimize for Minimal Changes

For migration and refactoring work:
- Small, reviewable changes
- One module or file at a time
- Add verification steps
- Create checkpoints with tests

### 10. Provide Complete File Revisions

When proposing changes to existing files:
- Always repeat the entire file without eliding
- Use `swift:filename` syntax to indicate file replacement
- Never skip over unchanged sections

## Decision Trees

### General Swift Development

```
What type of Swift development?

1. API Design & Naming?
   → Read swift-api-design-guidelines.md for conventions
   → Follow clarity-first principles

2. Platform-Specific Development?
   → Read Swift.md for platform guidance
   → Use appropriate frameworks (SwiftUI, UIKit, AppKit)

3. Testing?
   → Prefer Swift Testing framework over XCTest
   → For async code → swift-concurrency/testing.md

4. Concurrency & Threading?
   → See Concurrency Decision Tree below
```

### Concurrency-Specific Guidance

```
1. Starting fresh with async code?
   → Read swift-concurrency/async-await-basics.md
   → For parallel operations → swift-concurrency/tasks.md

2. Protecting shared mutable state?
   → Need to protect class-based state → swift-concurrency/actors.md
   → Need thread-safe value passing → swift-concurrency/sendable.md

3. Managing async operations?
   → Structured async work → swift-concurrency/tasks.md
   → Streaming data → swift-concurrency/async-sequences.md

4. Working with legacy frameworks?
   → Core Data integration → swift-concurrency/core-data.md
   → General migration → swift-concurrency/migration.md

5. Performance or debugging issues?
   → Slow async code → swift-concurrency/performance.md
   → Testing concerns → swift-concurrency/testing.md

6. Understanding threading behavior?
   → Read swift-concurrency/threading.md

7. Memory issues with tasks?
   → Read swift-concurrency/memory-management.md
```

### Common Error Triage

| Error/Warning | First Step | Reference File |
|---------------|------------|----------------|
| API naming unclear | Follow Swift conventions | swift-api-design-guidelines.md |
| Platform API confusion | Check platform-specific guidance | Swift.md |
| SwiftLint concurrency warnings | Check rule intent, avoid dummy awaits | swift-concurrency/linting.md |
| `async_without_await` | Remove async if not required; if required by protocol, use narrow suppression | swift-concurrency/linting.md |
| "Sending value of non-Sendable type risks causing data races" | Identify isolation boundary crossing | swift-concurrency/sendable.md |
| "Main actor-isolated ... cannot be used from nonisolated context" | Decide if it truly belongs on @MainActor | swift-concurrency/actors.md |
| "Class property 'current' is unavailable from asynchronous contexts" | Avoid thread-centric debugging | swift-concurrency/threading.md |
| XCTest async errors with `wait(...)` | Use `await fulfillment(of:)` or Swift Testing | swift-concurrency/testing.md |
| Core Data concurrency warnings | Use DAO pattern with NSManagedObjectID | swift-concurrency/core-data.md |

### Choosing the Right Concurrency Tool

```
Need thread-safe mutable state?
├─ Async context?
│  ├─ Single instance? → Actor
│  ├─ Global/shared? → Global Actor (@MainActor, custom)
│  └─ UI-related? → @MainActor
│
└─ Synchronous context?
   ├─ Can refactor to async? → Actor
   ├─ Legacy code integration? → Mutex
   └─ Fine-grained locking? → Mutex
```

## Reference Files

This power includes comprehensive guidance organized into steering files:

### General Swift Development

- **Swift.md** - Platform-specific guidance for iOS, macOS, watchOS, and visionOS development
- **swift-api-design-guidelines.md** - Swift API design conventions and naming guidelines

### Swift Concurrency (swift-concurrency/ directory)

- **async-await-basics.md** - async/await syntax, execution order, async let, URLSession patterns
- **tasks.md** - Task lifecycle, cancellation, priorities, task groups, structured vs unstructured
- **threading.md** - Thread/task relationship, suspension points, isolation domains, nonisolated
- **memory-management.md** - Retain cycles in tasks, memory safety patterns
- **actors.md** - Actor isolation, @MainActor, global actors, reentrancy, custom executors, Mutex
- **sendable.md** - Sendable conformance, value/reference types, @unchecked, region isolation
- **linting.md** - Concurrency-focused lint rules and SwiftLint patterns
- **async-sequences.md** - AsyncSequence, AsyncStream, when to use vs regular async methods
- **core-data.md** - NSManagedObject sendability, custom executors, isolation conflicts
- **performance.md** - Profiling with Instruments, reducing suspension points, execution strategies
- **testing.md** - XCTest async patterns, Swift Testing, concurrency testing utilities
- **migration.md** - Swift 6 migration strategy, closure-to-async conversion, @preconcurrency
- **glossary.md** - Quick definitions of core concurrency terms

## Best Practices

### API Design & Code Quality

1. **Follow Swift API Design Guidelines** - Write clear, grammatical code
2. **Clarity over brevity** - Include all words needed to avoid ambiguity
3. **Name based on roles** - Not types or implementation details
4. **Document public APIs** - Write clear documentation comments
5. **Use proper case conventions** - UpperCamelCase for types, lowerCamelCase for everything else

### Platform Development

6. **Prefer platform-native frameworks** - SwiftUI, UIKit, AppKit, Core Data
7. **Use official platform names** - iOS, iPadOS, macOS, watchOS, visionOS
8. **Avoid cross-platform API misuse** - Don't suggest iOS-only APIs for macOS
9. **Leverage Swift Testing** - Prefer modern testing framework over XCTest

### Concurrency & Safety

10. **Prefer structured concurrency** - Use task groups over unstructured tasks
11. **Minimize suspension points** - Keep actor-isolated sections small
12. **Use @MainActor judiciously** - Only for truly UI-related code
13. **Make types Sendable** - Enable safe concurrent access
14. **Handle cancellation** - Check Task.isCancelled in long-running operations
15. **Avoid blocking** - Never use semaphores or locks in async contexts
16. **Watch for reentrancy** - Don't assume state unchanged after await in actors
17. **Document escape hatches** - Always explain @preconcurrency, @unchecked Sendable

### Testing and Verification

18. **Test concurrent code** - Use proper async test methods
19. **Verify with Instruments** - Profile performance-related changes
20. **Check deinit behavior** - Verify lifetime and cancellation

## Migration Strategy

### Six Habits for Successful Migration

1. **Don't Panic—It's All About Iterations** - Break migration into small, manageable chunks
2. **Sendable by Default for New Code** - Make new types Sendable from the start
3. **Use Swift 6 for New Projects** - Enable Swift 6 language mode for new code
4. **Resist the Urge to Refactor** - Focus solely on concurrency changes
5. **Focus on Minimal Changes** - Small, focused pull requests
6. **Don't Just @MainActor All the Things** - Consider if main actor is truly appropriate

### Migration Steps

1. Find an isolated piece of code (standalone packages, individual files)
2. Update related dependencies to latest versions
3. Add async alternatives to closure-based APIs
4. Change default actor isolation (for app projects)
5. Enable strict concurrency checking (Minimal → Targeted → Complete)
6. Add Sendable conformances proactively
7. Enable Approachable Concurrency (Swift 6.2+) using migration tooling
8. Enable upcoming features individually
9. Change to Swift 6 language mode

### Migration Tooling

**Xcode**: Use Build Settings → Set upcoming feature to "Migrate" → Apply fix-its

**SwiftPM**: Use `swift package migrate --to-feature <FeatureName>`

Available migrations:
- `ExistentialAny` (SE-335)
- `InferIsolatedConformances` (SE-470)

## Common Patterns

### Network Request with UI Update

```swift
Task {
    let data = try await fetchData() // Background
    await MainActor.run {
        self.updateUI(with: data) // Main thread
    }
}
```

### Multiple Parallel Network Requests

```swift
async let users = fetchUsers()
async let posts = fetchPosts()
async let comments = fetchComments()
let (u, p, c) = try await (users, posts, comments)
```

### Processing Array Items in Parallel

```swift
await withTaskGroup(of: ProcessedItem.self) { group in
    for item in items {
        group.addTask { await process(item) }
    }
    for await result in group {
        results.append(result)
    }
}
```

### View Model with @MainActor

```swift
@MainActor
final class ContentViewModel: ObservableObject {
    @Published var items: [Item] = []
    
    func loadItems() async {
        items = try await api.fetchItems()
    }
}
```

## Verification Checklist

After making concurrency changes:

- [ ] Confirm build settings (default isolation, strict concurrency, upcoming features)
- [ ] Run tests, especially concurrency-sensitive ones
- [ ] Verify performance with Instruments (if performance-related)
- [ ] Verify deinit/cancellation behavior (if lifetime-related)
- [ ] Check for new warnings or errors
- [ ] Ensure UI updates happen on main thread
- [ ] Verify Sendable conformances are correct

## Additional Resources

This power is based on the comprehensive [Swift Concurrency Course](https://www.swiftconcurrencycourse.com?utm_source=github&utm_medium=agent-skill&utm_campaign=skill-footer) by Antoine van der Lee.

For video tutorials:
- [Approachable Concurrency Video](https://youtu.be/y_Qc8cT-O_g?si=y4C1XQDGtyIOLW81)
- [Migration Tooling Video](https://youtu.be/FK9XFxSWZPg?si=2z_ybn1t1YCJow5k)

## Support

For issues, questions, or contributions related to this power, please refer to the Swift Concurrency Course community or Apple's Swift forums.
