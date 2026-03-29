# Linux Kernel Driver Modernization Skill

A Claude skill for modernizing Linux kernel drivers with minimal, reversible changes.

## Overview

This skill helps developers modernize old Linux kernel drivers to work with newer kernels (5.x/6.x) using a "simple is better than everything" philosophy. It focuses on minimal, rollback-able, verifiable fixes.

## Features

- **Minimal Change Strategy**: Prioritize smallest possible changes that restore compilation
- **Reversible Fixes**: Each change is isolated and can be rolled back
- **Practical Approach**: Focus on compilation first, then runtime verification
- **Educational Resources**: Includes comprehensive Linux kernel labs documentation
- **Structured Navigation**: Clear indexing and organization of reference materials

## Directory Structure

```
kernel-dev-skill/
├── SKILL.md              # Main skill definition
├── README.md             # This file
├── references/           # Reference documentation
│   ├── source-map.md     # Navigation guide to educational content
│   ├── getting-started.md # Quick start guide (30-minute workflow)
│   └── api-migration-checklist.md # Prioritized API migration checklist
└── linux-kernel-labs-md/ # Educational content (93 markdown files)
    └── refs/heads/master/
        ├── index.md      # Main navigation index
        ├── lectures/     # 12 lecture files
        ├── labs/         # Practical lab exercises
        └── so2/          # Operating Systems 2 course
```

## Quick Navigation Guide

### When to Use This Skill

Use this skill when you encounter:
- Old drivers failing to compile on new kernels (5.x/6.x)
- Runtime probe failures, missing symbols, or structure field changes
- Need to migrate out-of-tree drivers to new APIs
- Need a "compile first, then gradually correct" transformation plan

### Reference Documents

1. **`references/source-map.md`** - Maps to specific educational content files
2. **`references/getting-started.md`** - 30-minute firefighting workflow
3. **`references/api-migration-checklist.md`** - Prioritized API migration issues

### Educational Content Index

The `linux-kernel-labs-md/` directory contains 93 markdown files organized as:

- **Lectures**: 12 theoretical topics (Introduction, Processes, Interrupts, SMP, Memory Management, etc.)
- **Labs**: Practical exercises (Device Drivers, Interrupts, Deferred Work, Filesystems, Networking, etc.)
- **SO2 Course**: Operating Systems 2 curriculum with labs and assignments

## Basic Workflow

1. **Reproduce and Baseline**: Run one full build, save original errors
2. **Fix by Priority**: Fix type/API/macro issues first, then semantic behavior
3. **Isolated Changes**: Make one type of change at a time, verify compilation
4. **Runtime Verification**: After compilation, test loading, probe, and basic IO
5. **Quality Checks**: Add static analysis and regression checklist

## Common Modernization Tasks

By frequency of occurrence:
- `file_operations`/`proc_ops` structure differences
- `timer_list` new interfaces and callback signature changes
- `get_user_pages*`, DMA mapping, memory API changes
- `irq` registration/release, `devm_*` resource management replacement
- `strlcpy`/`scnprintf`/`min_t` security interface replacements
- Kernel log level and `pr_*` normalization
- `of_*`/`acpi_*` matching and device tree compatibility fields

## Efficient Mode (30-minute Firefighting)

When you need to "put out the fire first, then improve":
- Run maximum 3 commands: `build`, `dmesg`, `grep`
- Output only the first 3 blocking issues and corresponding minimal fixes
- Each action must be "verifiable within 10 minutes"

## Contributing

This skill is designed to be practical and focused. Contributions that improve clarity, add useful examples, or enhance navigation are welcome.