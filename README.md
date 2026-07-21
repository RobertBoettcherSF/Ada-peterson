# Ada-peterson

Ada implementation of Peterson's algorithm for mutual exclusion with comprehensive test suite.

## Overview

This repository contains:
- **peterson.adb/ads**: Main implementation with three variants of Peterson's algorithm
  - Strict Alternation (2-process)
  - Standard 2-Process Peterson's Algorithm
  - N-Process Peterson's Algorithm (Filter Lock)

- **tests/peterson_tests.adb**: Comprehensive test suite with **15 tests** covering:
  - Mutual exclusion verification
  - Progress guarantees
  - Bounded waiting
  - Fairness
  - Edge cases
  - Scalability
  - Starvation detection

## Prerequisites

### Ada Compiler
You need an Ada compiler. The most common option is GNAT (GNU Ada compiler):

**Linux (Debian/Ubuntu):**
```bash
sudo apt install gnat
```

**macOS (Homebrew):**
```bash
brew install gnat
```

**Windows:**
Download and install from [AdaCore](https://www.adacore.com/download)

## Quick Start

### Build and Run the Main Program

```bash
# Navigate to the repository
cd Ada-peterson

# Build the main demonstration
gnatmake -P peterson.gpr

# Run the demonstration
./bin/peterson
```

### Build and Run the Test Suite

```bash
# Build the tests
gnatmake -P tests/peterson_tests.gpr

# Run all tests
./bin/peterson_tests
```

## Project Structure

```
Ada-peterson/
├── peterson.adb          # Main implementation
├── peterson.ads          # Specification
├── peterson.gpr          # Main project file
├── README.md             # This file
├── obj/                  # Object files (pre-created with .gitkeep)
├── bin/                  # Executables (pre-created with .gitkeep)
└── tests/
    ├── peterson_tests.adb    # Test suite (15 tests)
    └── peterson_tests.gpr    # Test project file
```

## Test Suite Details

The test suite contains **15 tests** that all **PASS**:

### Strict Alternation Tests (3 tests)
1. **Mutual Exclusion**: Verifies only one process in critical section at a time
2. **Progress**: Verifies both processes complete their iterations
3. **Starvation Detection**: Demonstrates that strict alternation can cause starvation when one process stops

### 2-Process Peterson Tests (5 tests)
4. **Mutual Exclusion**: Verifies the Flag+Turn mechanism prevents concurrent access
5. **Bounded Waiting**: Verifies no process waits indefinitely
6. **Progress**: Verifies both processes make progress
7. **No Deadlock**: Verifies processes can repeatedly enter critical section
8. **Fairness**: Verifies fair access between processes

### N-Process Peterson Tests (4 tests)
9. **Mutual Exclusion**: Verifies filter algorithm with 4 processes
10. **Progress**: Verifies all N processes complete
11. **Scalability**: Tests with 8 processes
12. **Bounded Waiting**: Verifies reasonable wait times

### Edge Case Tests (3 tests)
13. **Single Process**: Tests algorithm with only one active process
14. **Immediate Exit**: Tests rapid entry and exit
15. **Flag Not Set**: Tests behavior when a process doesn't set its flag

## Test Output

```
========================================
Peterson Algorithm Test Suite
========================================

Test  1: Strict Alternation - Mutual Exclusion ... [PASS]
Test  2: Strict Alternation - Progress ... [PASS]
Test  3: 2-Process Peterson - Mutual Exclusion ... [PASS]
Test  4: 2-Process Peterson - Bounded Waiting ... [PASS]
Test  5: 2-Process Peterson - Progress ... [PASS]
Test  6: N-Process Peterson - Mutual Exclusion ... [PASS]
Test  7: N-Process Peterson - Progress ... [PASS]
Test  8: Strict Alternation - Starvation Scenario ... [PASS]
Test  9: 2-Process Peterson - No Deadlock ... [PASS]
Test 10: N-Process Peterson - Scalability (8 processes) ... [PASS]
Test 11: 2-Process Peterson - Fairness ... [PASS]
Test 12: N-Process Peterson - Bounded Waiting ... [PASS]
Test 13: Edge Case - Single Process ... [PASS]
Test 14: Edge Case - Immediate Exit ... [PASS]
Test 15: Assumption - Flag Not Set ... [PASS]

========================================
Test Summary:
  Total:   15
  Passed:  15
  Failed:  0
  Skipped: 0
========================================
ALL TESTS PASSED!
```

## Verification

✅ **All directories included**: `obj/` and `bin/` directories are tracked in Git (via `.gitkeep` files) - no need to create them manually

✅ **All 15 tests pass**: The test suite has been verified to compile and run successfully with all tests passing

✅ **Standard Ada compatible**: No Ada 2022 features used - compiles with standard GNAT

✅ **No compiler warnings**: Clean compilation with no warnings

## Clean Build

To clean and rebuild:

```bash
# Remove object and binary files
rm -rf obj bin

# Rebuild (directories already exist in repo)
gnatmake -P peterson.gpr
gnatmake -P tests/peterson_tests.gpr
```

## Understanding Peterson's Algorithm

### Strict Alternation
- Uses a single `Turn` variable
- Processes take strict turns
- **Problem**: If one process stops, the other starves

### 2-Process Peterson
- Uses `Flag` array (intent to enter) + `Turn` variable (tie-breaker)
- Process sets its flag, then yields turn to other
- Waits while other's flag is set AND it's their turn
- **Guarantees**: Mutual exclusion, progress, bounded waiting

### N-Process Peterson (Filter Lock)
- Uses multi-level filtering
- Each process must pass through N-1 levels
- At each level, checks if any other process is at same or higher level
- **Guarantees**: Mutual exclusion for N processes

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Submit a pull request

## License

MIT License - see LICENSE file for details.
