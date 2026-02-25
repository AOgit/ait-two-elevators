# 🌾 Two Elevators — Java Multithreading

A **Java multithreading simulation** where trucks unload grain into two elevators simultaneously.

Homework #3 for the **Multithreading** lesson at **AIT TR GmbH**.

---

## 📋 Task

Rework the Elevator project from classwork so that:
- Trucks unload grain into **two elevators** instead of one
- During each trip, **half the grain** goes into elevator #1 and **half into elevator #2**
- The `Elevator.java` class **cannot be modified**
- **No grain loss** — every kernel must be accounted for
- Synchronization must be as **efficient as possible** (no unnecessary blocking)

---

## 🛠 Tech Stack

- Java
- Multithreading (`Runnable`, `Thread`)
- Synchronization (`synchronized`, `wait` / `notifyAll`)
- IntelliJ IDEA

---

## 🏗 Architecture

```
Truck (Thread)
    │
    ├── half load ──► ElevatorWorker #1 (Thread) ──► Elevator #1
    │
    └── half load ──► ElevatorWorker #2 (Thread) ──► Elevator #2
```

Multiple trucks run in parallel. Each truck splits its load exactly in half and notifies both elevator workers. Both halves are unloaded concurrently — neither elevator waits for the other.

---

## 🔑 Key Constraints

- `Elevator.java` is read-only — the synchronization logic lives entirely in `Truck` and the worker/dispatcher classes
- Grain split is exact — if the load is odd, one elevator gets `load/2` and the other gets `load - load/2` (no rounding loss)
- `wait` / `notifyAll` are used to coordinate between trucks and elevator workers without busy-waiting

---

## 📁 Project Structure

```
src/ait/elevator/
├── Elevator.java          # Provided class — cannot be edited
├── Truck.java             # Runnable — generates grain loads, splits them in half
├── ElevatorWorker.java    # Runnable — receives half-loads and adds to its Elevator
└── Main.java              # Entry point — creates trucks, workers, starts threads
```

---

## 🚀 Getting Started

```bash
git clone https://github.com/AOgit/ait-two-elevators.git
```

Open in **IntelliJ IDEA** and run `Main.java`.

The console will show each truck's delivery and the running totals in both elevators. At the end, the sum of both elevators equals the total grain delivered by all trucks.
