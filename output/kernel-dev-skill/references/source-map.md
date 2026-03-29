# Linux Kernel Labs Source Map

This document maps to the educational content converted from HTML to Markdown. Root directory:

`../linux-kernel-labs-md/`

## Quick Entry Points

- **Home Page**: `../linux-kernel-labs-md/index.md`
- **Main Document Index**: `../linux-kernel-labs-md/refs/heads/master/index.md`

## Core Lab Topics

### Complete Lab List
The `labs/` directory contains 15 lab files covering practical kernel development topics:

1. **Infrastructure**: `labs/infrastructure.md` - Development environment setup
2. **Introduction**: `labs/introduction.md` - Basic kernel concepts
3. **Kernel Modules**: `labs/kernel_modules.md` - Module loading/unloading
4. **Kernel API**: `labs/kernel_api.md` - Core kernel APIs
5. **Character Device Drivers**: `labs/device_drivers.md` - Character device implementation
6. **I/O Access and Interrupts**: `labs/interrupts.md` - Interrupt handling
7. **Deferred Work**: `labs/deferred_work.md` - Workqueues, tasklets, timers
8. **Block Device Drivers**: `labs/block_device_drivers.md` - Block device drivers
9. **Filesystem Drivers (Part 1)**: `labs/filesystems_part1.md` - VFS and basic filesystems
10. **Filesystem Drivers (Part 2)**: `labs/filesystems_part2.md` - Advanced filesystem topics
11. **Networking**: `labs/networking.md` - Network device drivers
12. **Kernel Development on ARM**: `labs/arm_kernel_development.md` - ARM-specific development
13. **Memory Mapping**: `labs/memory_mapping.md` - mmap and memory management
14. **Linux Device Model**: `labs/device_model.md` - Device tree and model
15. **Kernel Profiling**: `labs/kernel_profiling.md` - Performance analysis

### Key Labs for Driver Modernization
- **Character Devices**: `labs/device_drivers.md` - Sections 3-5 for driver structure
- **Interrupts**: `labs/interrupts.md` - Sections 2-4 for IRQ handling
- **Memory Mapping**: `labs/memory_mapping.md` - Sections 4-5 for mmap and DMA
- **Deferred Work**: `labs/deferred_work.md` - Sections 2-3 for timers and workqueues
- **Filesystems**: `labs/filesystems_part1.md` - Sections 2-3 for VFS integration
- **Networking**: `labs/networking.md` - Sections 3-4 for network drivers

## Lecture Materials

### Lecture Directory
`../linux-kernel-labs-md/refs/heads/master/lectures/`

### Key Lectures
- **Introduction**: `intro.md`
- **Processes**: `processes.md`
- **Interrupts**: `interrupts.md`
- **Memory Management**: `memory-management.md`
- **Networking**: `networking.md`
- **SMP and Synchronization**: `smp-and-synch.md`
- **Virtualization**: `virtualization.md`
- **Security**: `security.md`

### Complete Lecture List
The `lectures/` directory contains 12 lecture files covering:
1. Introduction to Kernel Programming
2. Processes and System Calls
3. Interrupts and Exceptions
4. SMP and Synchronization
5. Memory Management
6. Virtual Filesystem
7. Block Layer
8. Networking
9. Virtualization
10. Security
11. Debugging and Profiling
12. Kernel Development Process

## SO2 Course Materials

The `so2/` directory contains Operating Systems 2 curriculum materials:
- **Lab Assignments**: Practical exercises with solutions
- **Course Notes**: Detailed explanations of concepts
- **Reference Code**: Example implementations

## Usage Guidelines

### For API Migration
1. **Check lab documents first** for API migration clues and code patterns
2. **Use lecture documents** for background and theoretical context
3. **When encountering interface evolution issues**, prioritize locating code snippets in lab chapters of the same topic

### Navigation Strategy
- Start with `device_drivers.md` for basic driver modernization issues
- Consult `interrupts.md` and `deferred_work.md` for timing and concurrency issues
- Reference `memory_mapping.md` for DMA and memory API changes
- Use `filesystems_part1.md` for VFS and filesystem driver updates
- Check `networking.md` for network driver and socket API changes

### Quick Reference Paths
- **Basic Driver Structure**: `labs/device_drivers.md` → Section 3 (Character Devices)
- **Interrupt Handling**: `labs/interrupts.md` → Section 2 (Requesting IRQs)
- **Memory Operations**: `labs/memory_mapping.md` → Section 4 (mmap implementation)
- **Filesystem Basics**: `labs/filesystems_part1.md` → Section 2 (Registering Filesystems)

### Problem-to-File Mapping Table
Use this table to quickly locate documentation for specific issues:

| Problem Type | Primary File | Key Sections | Related Files |
|--------------|--------------|--------------|---------------|
| **File operations** | `labs/device_drivers.md` | 3. Character Devices, 4. File Operations | `lectures/fs.md` |
| **Interrupt handling** | `labs/interrupts.md` | 2. Requesting IRQs, 3. Interrupt Handlers | `lectures/interrupts.md` |
| **Timer/deferred work** | `labs/deferred_work.md` | 2. Tasklets, 3. Workqueues, 4. Timers | `lectures/smp.md` |
| **Memory mapping** | `labs/memory_mapping.md` | 4. mmap implementation, 5. DMA operations | `lectures/memory-management.md` |
| **Filesystem drivers** | `labs/filesystems_part1.md` | 2. Registering Filesystems, 3. File Operations | `labs/filesystems_part2.md` |
| **Network drivers** | `labs/networking.md` | 3. Network Devices, 4. Socket Operations | `lectures/networking.md` |
| **Device model** | `labs/device_model.md` | 2. Device Tree, 3. Platform Devices | `labs/arm_kernel_development.md` |
| **Kernel modules** | `labs/kernel_modules.md` | 2. Module Loading, 3. Module Parameters | `labs/introduction.md` |
| **Debugging** | `labs/kernel_profiling.md` | 2. Profiling Tools, 3. Debug Techniques | `lectures/debugging.md` |
| **ARM development** | `labs/arm_kernel_development.md` | 2. ARM Architecture, 3. ARM-specific APIs | `labs/device_model.md` |

## Content Statistics

- **Total Files**: 96 markdown files (based on file count)
- **Lectures**: 12 core lecture files + slide versions
- **Labs**: 15 lab files covering all major kernel topics
- **SO2 Materials**: Complete Operating Systems 2 course with labs and lectures
- **Conversion Source**: Originally from `linux-kernel-labs.github.io` HTML documentation
- **Structure**: Preserves original navigation with HTML-to-markdown conversion artifacts