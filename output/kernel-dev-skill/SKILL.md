---
name: kernel-dev-skill
description: Modernize Linux kernel drivers with minimal changes to restore compilation and runtime functionality. Use when users mention driver porting, kernel upgrade incompatibility, outdated APIs, DKMS, or probe/remove issues.
---

# Linux Kernel Driver Modernization

**Core Principle**: `Simple is better than everything`. Prioritize minimal, rollback-able, verifiable fixes.

## When to Use

Use this skill immediately in the following scenarios:
- Old drivers failing to compile on new kernels (e.g., 5.x/6.x)
- Runtime probe failures, missing symbols, structure field changes
- Need to migrate out-of-tree drivers to new APIs
- Need a "compile first, then gradually correct" transformation plan

## Input Checklist

First collect minimal necessary information to avoid over-analysis:
- Target kernel version and distribution
- Driver source path, `Kbuild/Makefile`
- First compilation errors (first 50 lines)
- Runtime key logs: corresponding module snippet in `dmesg`
- Hardware bus type (PCI/I2C/SPI/Platform/USB)

## Execution Order (Shortest Path)

1. First reproduce failure and freeze baseline: run only one full build, save original errors.
2. Fix by "compilation blocking priority": type/API/macro first, then semantic behavior.
3. Make only one type of change at a time and recompile, ensuring rollback capability.
4. After compilation passes, do minimal runtime verification (load, probe, basic IO).
5. Finally add static checks and regression checklist.

## Common Modernization Checklist

Check by frequency from high to low:
- `file_operations`/`proc_ops` structure differences
- `timer_list` new interfaces and callback signature changes
- `get_user_pages*`, DMA mapping, memory API changes
- `irq` registration/release, `devm_*` resource management replacement
- `strlcpy`/`scnprintf`/`min_t` security interface replacements
- Kernel log level and `pr_*` normalization
- `of_*`/`acpi_*` matching and device tree compatibility fields

## Minimal Change Strategy

- Compatibility layer first, then refactoring: prioritize thin wrapper macros/static inline functions, don't do major architectural changes first.
- No cross-file large migrations: single change limited to one theme.
- No premature optimization: make code correct first, then discuss performance and style unification.
- Use existing kernel helpers, don't reinvent the wheel.

## Diagnostic Commands

```bash
# Basic compilation
make -C /lib/modules/$(uname -r)/build M=$PWD V=1 modules
```

```bash
# Warnings and checks
make -C /lib/modules/$(uname -r)/build M=$PWD W=1 C=1 modules
```

```bash
# Sparse analysis
sparse -Wbitwise -Wcontext -Wcast-to-as -Wdefault-bitfield-sign -Wno-transparent-union
```

```bash
# Checkpatch
scripts/checkpatch.pl --strict --max-line-length=100 -f <changed_file.c>
```

```bash
# Coccinelle semantic patches
coccicheck MODE=report M=$PWD
```

```bash
# Kernel logs
dmesg -T | tail -n 200
```

## Output Template

Always output in this structure, keep it concise:

```text
# Modernization Plan
## 1) Build blockers (must-fix first)
## 2) Minimal patch set (ordered, reversible)
## 3) Runtime smoke checks
## 4) Regression risks
## 5) Next smallest step
```

## Quality Gates

- Must provide "minimal patch sequence", not generic suggestions.
- Each suggestion must map to specific error or log evidence.
- When uncertain, explicitly label assumptions, don't fabricate API details.
- Control output length: prioritize 5-12 high-value actions, avoid verbosity.

## Efficient Mode (30 minutes)

When user explicitly wants "firefighting first, then improvement", switch to efficient mode:
- Execute maximum 3 commands: `build`, `dmesg`, `grep`.
- Output only the first 3 blocking issues and corresponding minimal fixes.
- Each action must be "verifiable within 10 minutes".

## References

- **Navigation Guide**: `references/source-map.md` - Maps to educational content
- **Quick Start**: `references/getting-started.md` - 30-minute firefighting workflow
- **API Migration Checklist**: `references/api-migration-checklist.md` - Prioritized API issues
- **Educational Content**: `./linux-kernel-labs-md/` - 93 markdown files with lectures and labs