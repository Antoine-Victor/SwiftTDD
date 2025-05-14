# SwiftTDD

Creating a basic Stack class in Swift using Test-Driven Development (TDD) with the Swift Testing framework. We'll write tests first, then implement the Stack class to pass those tests. The Stack will support standard operations: push, pop, peek, and isEmpty.

### TDD Approach
1. Write a failing test for a specific behavior.
2. Implement the minimum code to make the test pass.
3. Refactor if needed, ensuring tests still pass.
4. Repeat for each feature.

### Step-by-Step

#### 1. Set Up the Project
- Create a new Swift project in Xcode.
- Ensure the Swift Testing framework is included (it’s built into Xcode 15+ for Swift 6).
- Create two files:
  - `Stack.swift` for the implementation.
  - `StackTests.swift` for the tests.

#### 2. Write Tests First
We’ll test the following Stack behaviors:
- Initialize an empty stack.
- Check if the stack is empty.
- Push elements onto the stack.
- Pop elements from the stack.
- Peek at the top element without removing it.
- Handle edge cases (e.g., pop/peek on an empty stack).

#### 3. Implementation
We’ll implement the Stack class to pass each test, following TDD principles.

Here’s the complete code, with tests and implementation, wrapped in artifacts as requested.

```swift
import Testing
@testable import StackModule // Replace with your module name

struct StackTests {
    @Test func testStackIsInitiallyEmpty() async throws {
        let stack = Stack<Int>()
        #expect(stack.isEmpty == true)
    }
    
    @Test func testPushMakesStackNonEmpty() async throws {
        var stack = Stack<Int>()
        stack.push(1)
        #expect(stack.isEmpty == false)
    }
    
    @Test func testPushIncreasesCount() async throws {
        var stack = Stack<Int>()
        stack.push(1)
        stack.push(2)
        #expect(stack.count == 2)
    }
    
    @Test func testPopReturnsLastPushedElement() async throws {
        var stack = Stack<Int>()
        stack.push(1)
        stack.push(2)
        let popped = stack.pop()
        #expect(popped == 2)
    }
    
    @Test func testPopMakesStackEmptyAfterLastElement() async throws {
        var stack = Stack<Int>()
        stack.push(1)
        _ = stack.pop()
        #expect(stack.isEmpty == true)
    }
    
    @Test func testPopOnEmptyStackReturnsNil() async throws {
        var stack = Stack<Int>()
        let popped = stack.pop()
        #expect(popped == nil)
    }
    
    @Test func testPeekReturnsLastPushedElementWithoutRemoving() async throws {
        var stack = Stack<Int>()
        stack.push(1)
        stack.push(2)
        let peeked = stack.peek()
        #expect(peeked == 2)
        #expect(stack.count == 2)
    }
    
    @Test func testPeekOnEmptyStackReturnsNil() async throws {
        let stack = Stack<Int>()
        let peeked = stack.peek()
        #expect(peeked == nil)
    }
}
```

```swift
public struct Stack<Element> {
    private var elements: [Element] = []
    
    public var isEmpty: Bool {
        elements.isEmpty
    }
    
    public var count: Int {
        elements.count
    }
    
    public mutating func push(_ element: Element) {
        elements.append(element)
    }
    
    public mutating func pop() -> Element? {
        elements.popLast()
    }
    
    public func peek() -> Element? {
        elements.last
    }
}
```

### Explanation of the Process
1. **Test: Empty Stack**
   - Wrote `testStackIsInitiallyEmpty` to verify a new stack is empty.
   - Implemented `Stack` with an `elements` array and `isEmpty` property to pass the test.

2. **Test: Push**
   - Added `testPushMakesStackNonEmpty` and `testPushIncreasesCount` to test pushing elements.
   - Implemented `push` to append elements and added `count` property to pass these tests.

3. **Test: Pop**
   - Wrote `testPopReturnsLastPushedElement`, `testPopMakesStackEmptyAfterLastElement`, and `testPopOnEmptyStackReturnsNil`.
   - Implemented `pop` using `popLast` to remove and return the last element, handling the empty case with `nil`.

4. **Test: Peek**
   - Added `testPeekReturnsLastPushedElementWithoutRemoving` and `testPeekOnEmptyStackReturnsNil`.
   - Implemented `peek` to return the last element without modifying the stack, returning `nil` for an empty stack.

### Running the Tests
- In Xcode, press `Cmd+U` to run the tests.
- Alternatively, use the terminal: `swift test` (ensure your project is set up for command-line testing).
- All tests should pass, confirming the Stack implementation is correct.

### Notes
- The Swift Testing framework uses `@Test` and `#expect` for assertions, making tests concise.
- The Stack is generic (`Stack<Element>`), allowing it to work with any type.
- Edge cases (e.g., popping/peeking an empty stack) return `nil` to avoid crashes.
- The implementation is minimal and efficient, using Swift’s `Array` for storage.

This TDD approach ensures the Stack is robust and well-tested.
