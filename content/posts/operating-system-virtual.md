---
title: "Virtual Memory: Concepts and Mechanisms"
date: 2025-12-15
author: "Max"
description: "Understanding virtual memory management, page tables, demand paging, and process isolation in operating systems"
tags: ["Operating Systems", "Virtual Memory", "Memory Management", "Page Table", "OS Concepts"]
---

The OS maps all data from disk into the virtual address space using **lazy loading** (demand paging). When a process tries to access a virtual page that isn't currently in physical memory, a **page fault** occurs, triggering the OS to load that page from disk into a physical frame.

---

## Logical Memory Components

- **page**: logical memory unit
- **page table**: data structure that converts virtual address to physical address

## Physical Memory Components

- **MMU**: memory management unit, translate virtual address to physical address in real time.
- **Frame**: physical memory unit

## Why virtual?

Continuous virtual space address is easy for OS to allocate memory for process, physical address is discrete(allocate, free memory, so you can imagine it is not continuous). And also for process isolation.

## Page Replacement

Frame is limited, when page fault occurs and memory is short, OS needs to decide which frame to swap. Typical algorithms like FIFO and LRU.

## Process Isolation

Process A and Process B each believe they have access to the entire memory space. Since each process has its own separate page table, the same virtual addresses in different processes map to different physical frames, ensuring process isolation.
