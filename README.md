# BarebonesOS

An experimental operating system built from scratch as a learning-first project.

## Project Roadmap

This roadmap is organized into practical milestones so the system can boot early, then evolve incrementally into a usable OS.

---

## Phase 0 — Project Foundation

### Goals
- Define architecture and core constraints.
- Set up development and debugging workflow.

### Decisions
- **CPU target**: x86_64
- **Firmware target**: UEFI
- **Bootloader**: Limine or GRUB (start with existing bootloader)
- **Primary dev environment**: QEMU (hardware testing later)
- **Language baseline**: C (with optional Rust components later)

### Deliverables
- Cross-compilation toolchain configured.
- Build script that produces bootable image.
- QEMU launch command and serial console logging.

---

## Phase 1 — Boot to Kernel Entry

### Goals
- Boot reliably into custom kernel code.
- Confirm control over early execution.

### Tasks
- Build kernel binary in proper format.
- Configure bootloader entries.
- Establish early console output (framebuffer and/or serial).

### Exit Criteria
- OS image boots in QEMU.
- Kernel prints deterministic startup banner.

---

## Phase 2 — Core CPU and Interrupt Bring-Up

### Goals
- Initialize fundamental CPU structures.
- Handle exceptions and hardware interrupts safely.

### Tasks
- Set up GDT/IDT and exception handlers.
- Configure PIC/APIC timer interrupt.
- Implement panic path and basic diagnostics.

### Exit Criteria
- Timer interrupts fire consistently.
- Exceptions produce readable debug output.

---

## Phase 3 — Memory Management

### Goals
- Introduce robust physical and virtual memory control.

### Tasks
- Parse firmware memory map.
- Implement physical page frame allocator (PMM).
- Implement virtual memory manager (VMM) + paging.
- Establish kernel heap allocator.

### Exit Criteria
- Dynamic memory allocation available in kernel.
- Page mapping/unmapping tested for correctness.

---

## Phase 4 — Tasking and Scheduling

### Goals
- Add basic multitasking.

### Tasks
- Define process and thread structs.
- Implement context switching.
- Add simple round-robin scheduler.

### Exit Criteria
- Multiple kernel threads run cooperatively/preemptively.
- Scheduler can switch tasks on timer interrupts.

---

## Phase 5 — Syscalls and User Mode

### Goals
- Create user/kernel boundary and syscall interface.

### Tasks
- Enter user mode safely.
- Implement minimal syscall mechanism (e.g., write, exit).
- Define stable syscall numbering conventions.

### Exit Criteria
- A tiny user program can execute and print output through syscalls.

---

## Phase 6 — Filesystem and VFS

### Goals
- Provide file abstractions and persistent storage path.

### Tasks
- Start with initramfs/ramfs.
- Add VFS layer with file handles and path resolution.
- Integrate a simple disk-backed filesystem (e.g., FAT/ext2 later).

### Exit Criteria
- Kernel can open/read basic files via VFS.

---

## Phase 7 — Drivers and Device Model

### Goals
- Standardize hardware access and driver lifecycle.

### Tasks
- Define driver interface and registration model.
- Add essential drivers: timer, keyboard, storage, console.
- Add PCI scanning and device discovery.

### Exit Criteria
- System can interact with keyboard and persistent block device.

---

## Phase 8 — Userland Base System

### Goals
- Boot into minimal usable environment.

### Tasks
- Create init process.
- Add basic shell and core utilities.
- Define executable loading format and loader behavior.

### Exit Criteria
- System boots into shell prompt and runs simple commands.

---

## Phase 9 — Reliability, Security, and Tooling

### Goals
- Improve stability, debugability, and safety.

### Tasks
- Add kernel assertions, logging levels, and crash reports.
- Add basic hardening (W^X policy, pointer validation).
- Build regression tests for core subsystems.

### Exit Criteria
- Repeatable test workflow in CI/QEMU.
- Fewer silent failures; improved diagnosability.

---

## Phase 10 — Networking (Optional Advanced Track)

### Goals
- Introduce network stack incrementally.

### Tasks
- Add NIC driver foundation.
- Implement minimal packet handling.
- Progress through ARP, IPv4, ICMP, then TCP/UDP basics.

### Exit Criteria
- Ping support and simple network communication demo.

---

## Suggested Milestone Order (Short Version)
1. Boot and print text.
2. Interrupts + timer.
3. Memory allocators.
4. Scheduler.
5. User mode + syscalls.
6. VFS + filesystem.
7. Drivers.
8. Shell + utilities.
9. Hardening/tests.
10. Networking.

## Definition of Done for Each Milestone
- Feature implemented.
- Demo reproducible in QEMU.
- Debug logs included.
- Basic test or validation script added.
- README progress checklist updated.

## Progress Checklist
- [ ] Phase 0 — Project Foundation
- [ ] Phase 1 — Boot to Kernel Entry
- [ ] Phase 2 — Core CPU and Interrupt Bring-Up
- [ ] Phase 3 — Memory Management
- [ ] Phase 4 — Tasking and Scheduling
- [ ] Phase 5 — Syscalls and User Mode
- [ ] Phase 6 — Filesystem and VFS
- [ ] Phase 7 — Drivers and Device Model
- [ ] Phase 8 — Userland Base System
- [ ] Phase 9 — Reliability, Security, and Tooling
- [ ] Phase 10 — Networking (Optional Advanced Track)
