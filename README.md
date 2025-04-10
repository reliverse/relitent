# Relitent OS

> A hobby operating system written in Rust/C/C++.

## Hypothetical Development Roadmap

### 1. **Research & High-Level Planning**

- [ ] **Define The OS Vision**  
  - [ ] Clarify if this will be a **bare-metal hobby OS** or built on an existing kernel (Linux/BSD).  
  - [ ] Choose the target use case (educational, embedded, desktop, etc.).  
  - [ ] Decide on core architecture (x86_64, ARM, RISC-V).
- [ ] **Set Up Toolchain**  
  - [ ] Configure a cross-compiler or specialized toolchain (GCC/Clang) for the target architecture.  
  - [ ] Create a basic build system (e.g., Make/CMake, or custom scripts).

### 2. **Bootloader & Basic Startup**

- [ ] **Bootloader**  
  - [ ] Pick or write a minimal bootloader (e.g., GRUB, Limine, or a custom stage-2 loader).  
  - [ ] Ensure it loads the kernel image into memory and sets up a correct environment (registers, memory map).
- [ ] **Kernel Entry Point**  
  - [ ] Set up an entry function in assembly or C/C++ that initializes basic hardware state.  
  - [ ] Switch to protected mode / long mode (x86_64) if needed.  
  - [ ] Initialize the stack and global descriptor table (GDT) or memory management unit (MMU) structures.

- [ ] **Basic Print/Debug**  
  - [ ] Implement a low-level printing function (e.g., to VGA text buffer on x86, or a serial port).  
  - [ ] Provide a minimal “Relitent OS” message to confirm boot success.

### 3. **Kernel Foundations**

- [ ] **Interrupts & Exceptions**  
  - [ ] Set up the Interrupt Descriptor Table (IDT) and handle CPU exceptions (divide by zero, invalid opcode).  
  - [ ] Provide a stub to handle hardware interrupts (e.g., keyboard, timer).

- [ ] **Memory Management**  
  - [ ] Implement physical memory management (PMM) to track free/used RAM.  
  - [ ] Implement a simple paging system / virtual memory (VMM).  
  - [ ] Basic heap allocator (kmalloc/kfree) for kernel dynamic allocations.

- [ ] **Scheduler & Process Model**  
  - [ ] If you’re implementing a **multitasking** kernel, define tasks/threads, a scheduling algorithm (round-robin or priority-based).  
  - [ ] Provide a minimal system call interface for processes to spawn, exit, do I/O, etc.

- [ ] **Driver Framework**  
  - [ ] Outline a system to register/unregister drivers.  
  - [ ] Possibly a simple device model (e.g., devfs or a device tree).

### 4. **Essential Drivers & Hardware Support**

- [ ] **Timer/Clock**  
  - [ ] Use the PIT/APIC (on x86) or a platform-specific timer on ARM.  
  - [ ] Provide system ticks for scheduling, timekeeping.

- [ ] **Keyboard**  
  - [ ] PS/2 or USB keyboard driver to capture user input.  
  - [ ] Basic scancode to ASCII translation table.

- [ ] **Display / Console**  
  - [ ] If text-mode: continue with VGA or a simple frame buffer.  
  - [ ] If we want early GUI: initialize a linear frame buffer for drawing pixels in a basic 2D environment.

- [ ] **Mass Storage** (Optional for V1, but often needed)  
  - [ ] Implement an IDE or AHCI driver for disks (if x86).  
  - [ ] Minimal read/write routines to load OS data from a disk partition or image.

- [ ] **Network** (Optional for V1)  
  - [ ] If we want basic networking, implement an Ethernet driver + minimal TCP/IP stack or rely on a simpler approach for a future version.

### 5. **Filesystem & I/O**

- [ ] **Filesystem Drivers**  
  - [ ] Decide on a default filesystem (FAT32, ext2, or a custom minimal FS).  
  - [ ] Implement mounting, reading directories, reading/writing files.  
  - [ ] Provide a user-facing path API (e.g., `/`, `/dev`, etc.).
- [ ] **User-Space I/O**  
  - [ ] If we have a userland, define syscalls or library functions for open, read, write, close.  
  - [ ] Possibly implement a virtual `/dev` for device file access.

### 6. **User Space & Shell**

- [ ] **Process Launching**  
  - [ ] Provide a mechanism to load and start a user-space program from the filesystem.  
  - [ ] Implement a simple ELF or custom executable loader.

- [ ] **C Library / Runtime**  
  - [ ] Provide a minimal C library or newlib-like environment for user programs.  
  - [ ] Basic stdio (printf, etc.), memory allocation, string functions.

- [ ] **Shell / Command Interface**  
  - [ ] A minimal shell (text-based) to run commands (e.g., `ls`, `cat`, `echo`).  
  - [ ] Possibly embedded in the kernel for V1, or a separate user-space binary.

### 7. **Minimal GUI Environment** (Optional for V1)

- [ ] **Windowing System**  
  - [ ] Implement a simple window manager in user-space or kernel-space.  
  - [ ] Provide basic drawing APIs (bitmaps, lines, fonts).
- [ ] **Input Handling**  
  - [ ] Route keyboard/mouse events to the GUI environment.  
  - [ ] Simple event system: click, keypress, focus.

- [ ] **Demo Applications**  
  - [ ] A small “paint” or “notepad” app to show off the GUI capabilities.  
  - [ ] Possibly a “file manager” or “app launcher.”

### 8. **Installer & Distribution** (Optional for V1)

- [ ] **Bootable ISO/USB**  
  - [ ] Provide a script or tool to package the kernel + userland into a bootable ISO image (GRUB or another bootloader).  
  - [ ] Optionally let users write to a USB flash drive.

- [ ] **Partition / Install Script**  
  - [ ] If we want an “installer,” create a minimal script that formats a partition and copies OS files.  
  - [ ] More advanced if we want a fully guided installer.

### 9. **Updates & Package Management** (Likely beyond V1)

- [ ] **Manual Rebuild**  
  - [ ] Start with a manual approach: re-compile the OS + kernel and replace the image.  
  - [ ] Provide a stable “release image” for others to try.

- [ ] **Online Updates** (Optional)  
  - [ ] Consider a package manager or OS-level update mechanism for future expansions.  
  - [ ] This is typically advanced territory.

### 10. **Security & Permissions** (Basic for V1)

- [ ] **User/Group Model** (Optional)  
  - [ ] If we want multi-user, define user IDs, group IDs, file permission bits.  
  - [ ] Provide minimal authentication or skip for single-user mode in V1.

- [ ] **Basic Security**  
  - [ ] Ensure we handle CPU exceptions safely.  
  - [ ] Avoid kernel panics on invalid memory accesses.  
  - [ ] Possibly integrate a stack canary or ASLR if you’re advanced.

### 11. **Testing & Validation**

- [ ] **Unit Tests**  
  - [ ] For kernel components (memory manager, driver code).  
  - [ ] Possibly a minimal in-kernel test framework or userland test suite.

- [ ] **Integration / End-to-End**  
  - [ ] Boot the OS in QEMU/Bochs/VirtualBox to test real boot flow.  
  - [ ] Validate file read/write, driver stability, interrupts, scheduling.

- [ ] **Manual Testing**  
  - [ ] Boot on real hardware (if feasible) to catch driver or timing issues.  
  - [ ] Document known limitations (lack of certain drivers, partial features).

### 12. **Documentation & Community**

- [ ] **Write a Developer Guide**  
  - [ ] Summarize the OS architecture, how to build, how to add drivers.  
  - [ ] Explain major design choices (kernel model, memory layout, system calls).
- [ ] **User Guide**  
  - [ ] Basic usage: how to boot, run the shell, list files, run a simple text editor or app.  
  - [ ] If we have a GUI, instructions on usage or shortcuts.
- [ ] **Community / Feedback**  
  - [ ] Possibly open source the project on GitHub/GitLab.  
  - [ ] Encourage other hobby OS devs to contribute or experiment.

### 13. **Roadmap for Future Versions**

- [ ] **Expand Hardware Support** (Network drivers, USB devices, GPU acceleration).
- [ ] **Advanced Features** (sophisticated GUI, multi-user security, package manager).
- [ ] **Performance Optimizations** (more efficient scheduling, deeper driver improvements).
- [ ] **Porting Common User Apps** or building a bigger userland (shell tools, compilers, browsers).
- [ ] **Refining the Architecture** (64-bit only, advanced memory protections, SMP, etc.).
