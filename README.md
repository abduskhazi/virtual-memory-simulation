# Virtual Memory Simulation

> A Java-based simulation of **virtual memory, page replacement, and process memory access**.

This project explores how an operating system manages memory when multiple processes access virtual pages, with a focus on **page faults and page replacement**.

```text id="eb8k4m"
Process Memory Access
        ↓
    Page Lookup
        ↓
   Page Fault?
      /    \
    No      Yes
    │        │
    │   Page Replacement
    │        │
    └────────┘
        ↓
 Continue Execution
```

## Highlights

* Simulates **multiple processes and page accesses**
* Models **page replacement using the Clock algorithm**
* Includes two implementations:

  * **Simple Clock**
  * **Complex Clock**
* Uses configurable input describing processes, read/write operations, and accessed locations
* Compares replacement behavior through the resulting **page-fault count**

The original experiments showed that, for larger inputs, the complex Clock implementation produced fewer page faults than the simple variant.

## Project Structure

```text id="h0cr9q"
OS_clockSimple/     # Simple Clock replacement
OS_ComplexClock/    # Complex Clock replacement
```

Each version contains the Java sources needed to run that simulation.

## Input

The simulator consumes records of the form:

```text id="3k2r1c"
ProcessesNumber, Read/Write operation, Memory location
```

For example, the input describes which process is accessing memory and where that access occurs.

## Why this project?

The project was built to understand the interaction between **virtual memory, page faults, page replacement, and process memory access** by implementing the mechanisms as an executable simulation rather than studying them only theoretically.

**Abdus Salam Khazi · Abhishek A. R. · Abhishek Patil · Akshay Mallya**
