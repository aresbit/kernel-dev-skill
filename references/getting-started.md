# Getting Started (Driver Modernization)

## Goal

Get old drivers from "compilation failure" back to "compilable, loadable, basic verifiable" in the shortest time possible.

## 30-Minute Firefighting Process

### 1. Save Baseline Errors
- `make -C /lib/modules/$(uname -r)/build M=$PWD V=1 modules > build.log 2>&1`
- Capture only the first 50 lines of the first error chain.

### 2. Identify First Blockers
- Fix type/macro/function signature changes first.
- Temporarily ignore style warnings and performance optimizations.

### 3. Single-Theme Changes + Recompilation
- Fix only one type of problem at a time.
- Immediately verify with `make` after each change.

### 4. Minimal Runtime Verification
- `insmod` or `modprobe`
- Check `dmesg` for `probe`/`remove`/irq key logs

## What NOT to Do

- **Don't do large-scale refactoring** in the first migration round.
- **Don't guess API behavior** without evidence.
- **Don't make changes across multiple modules** simultaneously.
- **Don't optimize prematurely** - correctness first, performance later.
- **Don't ignore rollback capability** - each change should be reversible.