# ExPResSO : Experimental Parallel Resource Scheduler and Organizer ☕

**ExPResSO** is a lightweight parallel programming library in C, designed to simplify multi-core architecture exploitation. Inspired by OpenMP concepts, it implements a custom runtime engine based on the **Fork-Join** paradigm.

This project was developed as part of the Master 1 curriculum (Internal OS Architecture).

## 🚀 Key Features

*   **Thread Pool Management:** Automatic creation of a worker team adapted to the machine's core count.
*   **Task Engine:** Asynchronous task submission via a thread-safe linked-list queue.
*   **Scheduling Policies:**
    *   `DYNAMIC`: First-Come, First-Served distribution (Default).
    *   `STATIC`: Round-Robin distribution.
    *   `BALANCED`: Load balancing based on task weight estimation.
*   **Optimized Synchronization:** Active `wait` barrier where the main thread contributes to the computation to minimize idle time.

## 🛠️ Tech Stack

This project is built from scratch using low-level concepts:
*   **Language:** C (C99 Standard)
*   **Concurrency:** POSIX Threads (`pthreads`)
*   **Synchronization:** Mutexes & Condition Variables
*   **Memory Management:** Dynamic allocation strategies to prevent leaks.

## 📦 Build & Install

### Prerequisites
*   GCC Compiler
*   Make
*   Linux/Unix Environment

### 1. Build and Install the Library
```bash
# Clone the repository
git clone https://github.com/amarlechani1-w/ExPResSO-Parallel-Library.git
cd ExPResSO-Parallel-Library/expresso

# Compile and install to a local directory
PREFIX=$HOME/expresso_install make install
```

### 2. Run the Benchmarks
```bash
cd ../expresso-benchmarks
# Ensure the Makefile points to your installation path if needed
make
```

## ⚡ Performance Results

The library has been validated against sequential implementations on intensive workloads.
*Results obtained on an 8-core machine:*

| Benchmark | Description | Dataset Size | Speedup |
| :--- | :--- | :--- | :--- |
| **VECMUL** | Vector Multiplication | 50 Million elements | **x 4.7** |
| **MATMUL** | Matrix Multiplication | 1000x1000 | **x 2.6** |
| **LIST** | Linked-List Processing | Heterogeneous tasks | **Time divided by 3** |

*Note: On small datasets, a slight overhead is observed due to thread management costs, demonstrating the theoretical limits of parallelism (Amdahl's Law).*

## 💻 Usage Example

The API is designed to be simple and user-friendly:

```c
#include "expresso.h"

// 1. Initialize the engine
expresso_initialize();

// 2. Submit tasks
for(int i=0; i<num_tasks; i++) {
    // Send a function pointer and its data
    expresso_weighted_task(my_function, &my_data[i], weight);
}

// 3. Wait for completion (Barrier)
expresso_wait();

// 4. Cleanup resources
expresso_finalize();
```

## ⚙️ Advanced Configuration

You can control the runtime behavior using environment variables without recompiling:

```bash
# Force usage of 4 threads and Balanced scheduling policy
EXPRESSO_WORKER_COUNT=4 EXPRESSO_SCHEDULE=balanced ./my_program
```

## 👤 Author

**Amar LECHANI**
*   Master 1 Student - ISTY/CHPS

---
*This project demonstrates proficiency in System Programming, Concurrency, and Performance Optimization.*
