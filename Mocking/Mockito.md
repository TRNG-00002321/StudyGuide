# Mockito

## Test Doubles
Test doubles are general-purpose replacements for real objects used during testing.
They let you isolate the code under test so you don’t rely on real databases, APIs, services, or slow/complex components.

### Types of test doubles
There are 5 commonly referenced categories  
**1. Dummy :** Used only to fill parameter lists. They are never used by the code under test.  
    _Example:_ passing null or an empty object when you must supply something.

**2. Stub :** Provides predefined answers to calls. Used when the code under test needs some data but you don’t care about interactions.  
    _Example:_ A stubbed database that always returns a fixed user.

**3. Fake :** A working but simplified implementation that behaves like the real thing, but is suitable for tests.  
    _Example:_ An in-memory database instead of a real SQL server.

**4. Mock :** A fake object that also records how it was used so the test can verify interactions.  
    _Example:_ A mock email service that checks your code called send(email) exactly once.

**5. Spy :** Similar to a mock but usually less strict; it records interactions passively and you assert on them later.  
    _Example:_ A spy logs what methods were called; the test checks the spy afterward.

### Comparison 
| Type  | Returns data?  | Tracks calls? | Behavior                   |
| ----- | -------------- | ------------- | -------------------------- |
| Dummy | No             | No            | Fills params only          |
| Stub  | Yes (fixed)    | No            | Simple data provider       |
| Fake  | Yes (real-ish) | No            | Lightweight implementation |
| Mock  | Yes/No         | Yes (strict)  | Checks interactions        |
| Spy   | Yes/No         | Yes (passive) | Records interactions       |

## Stubbing
Stubbing in testing is the practice of replacing a real function, method, or dependency with a controlled version (a stub) that returns predefined data.  
Stubs help you isolate the unit under test by giving it predictable inputs—without requiring real databases, APIs, networks, or other complex systems.
### A stub:
- Returns fixed, pre-programmed values
- Does not contain real logic
- Does not verify how it was called (that’s mocking)
- Helps make tests fast, deterministic, and isolated
### Use a stub when:
- You need to control the data a dependency returns.
- You don’t care about the dependency’s internal behavior.
- You want to simulate normal or edge-case conditions easily.

***Examples :***
- Returning a known user from a fake repository
- Providing a fixed timestamp from a clock
- Simulating an API returning an error response

## Mocking
In unit testing, mocking is the practice of replacing real objects or functions with fake, controlled versions (called mocks) so you can test a piece of code in isolation.
When unit testing, you want to test one small unit of logic at a time, without depending on:
- Databases
- Networks / APIs
- File systems
- Time / random behavior
- Other complex objects

**Mocks let you simulate these dependencies with predictable behavior.** 
### Mocks can:
- Return predefined values
- Track how they were used (e.g., “Was this function called?”)
- Simulate errors or exceptions
- Validate interactions (e.g., “Was it called with the right arguments?”)

### Stubs Vs Mocks

| Feature                   | Stub  | Mock    |
| ------------------------- | ----- | ------- |
| Returns predefined values | Yes | Maybe |
| Tracks calls              | No  | Yes   |
| Used for isolation        | Yes | Yes   |
| Used to verify behavior   |  No  | Yes   |

### Comparison

| Feature  | Stubbing                            | Mocking                       |
| -------- | ----------------------------------- | ----------------------------- |
| Purpose  | Provide predictable return values   | Verify that calls happened    |
| Example  | `when(api.fetch()).thenReturn(...)` | `verify(api).fetch()`         |
| Focus    | State-based testing                 | Behavior-based testing        |
| Use case | Testing logic that depends on data  | Ensuring correct interactions |
