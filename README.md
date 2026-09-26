# Virtual Memory Simulation

> Built to understand virtual memory by implementing the machinery — not just algorithms, but the coordination between scheduling, fault handling, and translation that a real kernel does every millisecond.

---

## Memory View

```
PHYSICAL MEMORY (solid frames)
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┐
│Frame0│Frame1│Frame2│Frame3│Frame4│Frame5│Frame6│Frame7│ ...
│ P1   │ P3   │ P1   │ P2   │ free │ P3   │ P1   │ free │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┘
   ▲       ▲       ▲       ▲       ▲       ▲       ▲       ▲
   │       │       │       │       │       │       │       │
   └───────┴───────┴───────┴───────┴───────┴───────┴───────┘
                       │
                       ▼ maps via page tables
VIRTUAL MEMORY (dotted = per-process address space)

  Process 1          Process 2          Process 3          Process N
  ───────────        ───────────        ───────────        ───────────
  VP 0 ──·····│──► Frame0
  VP 1 ──·····│──► Frame2
  VP 2 ──·····│──► Frame6
  VP 3 ──·····│
  ...                           ...                ...                ...

Each process: 64-entry page table (VPN→PFN), initially all invalid ("0000000000000000")
```

---

## Kernel Subsystems

```
         ┌────────────────┬────────────────┐
         ▼                ▼                ▼
┌───────────────┐ ┌───────────────┐ ┌───────────────┐
│   SCHEDULER   │ │ PAGE FAULT    │ │    MMU        │
│ • round-robin │ │ • Clock alg   │ │ • vaddr→paddr │
│ • picks PID   │ │ • frame table │ │ • walks PTEs  │
└───────────────┘ └───────────────┘ └───────────────┘
```

---

## Two Replacement Policies

| Dir | Policy | Evicts |
|-----|--------|--------|
| `OS_clockSimple/` | Simple Clock | Oldest unreferenced |
| `OS_ComplexClock/` | Complex Clock | Oldest unreferenced **clean** |

---

## Run (30 sec)

```bash
cd OS_clockSimple && javac *.java && java Main
# memory size (4–16 KB) → input file
```

Outputs: scheduler picks, page faults, frame table, final fault count.

---

**Authors**: Abdus Salam Khazi · Abhishek A. R. · Abhishek Patil · Akshay Mallya  
**Contact**: abduskhazi@gmail.com