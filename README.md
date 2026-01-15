# Swift 6 Expert Power for Kiro

Expert guidance for Swift 6 development on Apple platforms. This Kiro power provides comprehensive support for modern Swift programming, including language features, API design, concurrency patterns, and best practices.

## What This Power Provides

- **Swift 6 Language Features** - Modern syntax, strict concurrency, and migration strategies
- **API Design Guidelines** - Write clear, idiomatic Swift code following Apple's conventions
- **Concurrency Expertise** - Deep knowledge of async/await, actors, tasks, and Sendable
- **Platform Development** - iOS, iPadOS, macOS, watchOS, and visionOS guidance
- **Testing Support** - Swift Testing framework and async testing patterns
- **Framework Integration** - SwiftUI, UIKit, AppKit, Core Data, and more

## Who Should Use This Power

This power is ideal for developers who:

- Are migrating to Swift 6 or enabling strict concurrency checking
- Want to write idiomatic, well-designed Swift APIs
- Need help with async/await, actors, or data race safety
- Are building apps for Apple platforms
- Want to follow Swift best practices and conventions
- Need guidance on testing concurrent code

## What's Included

### Core Documentation

- **POWER.md** - Main power documentation with agent behavior guidelines
- **swift.md** - Platform-specific guidance for Apple ecosystem development
- **swift-api-design-guidelines.md** - Comprehensive API design conventions

### Swift Concurrency Deep Dive

The `steering/swift-concurrency/` directory contains 13 detailed guides covering:

- Async/await fundamentals and patterns
- Actors, @MainActor, and isolation
- Tasks, task groups, and structured concurrency
- Sendable conformance and type safety
- Threading model and suspension points
- Memory management in concurrent code
- Performance optimization with Instruments
- Testing async code
- Core Data integration
- Migration strategies for Swift 6
- Linting and code quality
- AsyncSequence and streaming data

## Quick Start

1. **Install the Power** in Kiro through the Powers panel
2. **Mention Swift topics** in your chat - the power activates automatically on keywords like:
   - swift, swift6, async, await, actor, sendable
   - ios, macos, swiftui, api-design
   - concurrency, migration, testing
3. **Get Expert Guidance** - The agent will reference the appropriate steering files for your specific needs

## Example Use Cases

### API Design
```swift
// Get guidance on naming conventions and Swift idioms
"How should I name this method that removes items from a collection?"
```

### Concurrency
```swift
// Learn about actor isolation and data race safety
"I'm getting a Sendable warning when passing this class to an actor"
```

### Migration
```swift
// Step-by-step Swift 6 migration help
"How do I enable strict concurrency checking in my project?"
```

### Testing
```swift
// Modern testing patterns
"How do I test this async function with Swift Testing?"
```

## Key Features

### Intelligent Guidance

The power provides context-aware recommendations:
- Analyzes your project settings (Swift version, concurrency level)
- Identifies isolation boundaries before suggesting fixes
- Recommends minimal, reviewable changes
- Avoids blanket solutions like adding @MainActor everywhere

### Comprehensive Coverage

From basics to advanced topics:
- Simple async/await conversions
- Complex actor reentrancy scenarios
- Custom actor executors
- Region-based isolation
- Migration tooling and strategies

### Best Practices Built-In

Follows established Swift conventions:
- Swift API Design Guidelines
- Apple platform idioms
- Structured concurrency patterns
- Modern testing approaches

## Attribution

The Swift Concurrency content is based on the comprehensive [Swift Concurrency Course](https://www.swiftconcurrencycourse.com) by Antoine van der Lee.

Swift API Design Guidelines content is adapted from [Swift.org API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/).

## Installation

1. Open Kiro IDE
2. Navigate to the Powers panel
3. Click "Add Custom Power"
4. Enter this repository URL: `https://github.com/sebsto/swift-kiro-power`
5. Click Add

The power will be installed and automatically activated when you mention relevant Swift keywords in your conversations.

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests to improve the documentation and guidance.

## License

See [LICENSE.txt](LICENSE.txt) for details.

## Support

For questions about using this power or Swift 6 development:
- Check the detailed steering files in this repository
- Visit the [Swift Concurrency Course](https://www.swiftconcurrencycourse.com)
- Consult Apple's official Swift documentation
