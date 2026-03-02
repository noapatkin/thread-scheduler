User-Level Threads Library (C++)

Overview

This project implements a user-level threading library in C++, providing preemptive context switching and round-robin scheduling without relying on OS kernel threads.

The library manages multiple user threads within a single process using:

-setjmp / longjmp for context switching

-SIGVTALRM virtual timer signals

-Custom scheduling and thread state management

-This project demonstrates low-level systems programming concepts including signal handling, stack management, and cooperative/preemptive multitasking.

Features

-Preemptive round-robin scheduler

-Configurable quantum length (microseconds)

Thread lifecycle management:

-uthread_spawn

-uthread_terminate

-uthread_block

-uthread_resume

-uthread_sleep

-Per-thread quantum tracking

-Global quantum counter

-Fixed maximum number of concurrent threads

Architecture

Thread Representation

Each thread includes:

-Thread ID

-Execution state (RUNNING, READY, BLOCKED)

-Private stack

-Saved execution context (sigjmp_buf)

-Quantum execution counter

Scheduler

The scheduler manages:

-Ready queue (FIFO round-robin)

-Sleeping threads map

-Available thread IDs (min-heap)

-Currently running thread

-Virtual timer configuration

-Context Switching

-Context switching is implemented using:

-sigsetjmp to save thread state

-siglongjmp to restore thread state

-setitimer(ITIMER_VIRTUAL) for quantum-based preemption

Thread States

-RUNNING – Currently executing thread

-READY – Waiting in ready queue

-BLOCKED – Suspended until resumed

-Sleeping threads are tracked separately with a quantum countdown

API Summary

-int uthread_init(int quantum_usecs);

-int uthread_spawn(thread_entry_point entry_point);

-int uthread_terminate(int tid);

-int uthread_block(int tid);

-int uthread_resume(int tid);

-int uthread_sleep(int num_quantums);

-int uthread_get_tid();

-int uthread_get_total_quantums();

-int uthread_get_quantums(int tid);

Purpose

This project was developed as part of a systems programming course to gain hands-on experience with:

-Operating system principles

-Context switching internals

-Timer-based scheduling

-Memory and signal handling in C++
