*This project has been created as part of the 42 curriculum by megrelli.*

## 💡 Description

Philosophers is a C programming project whose goal is to solve the classic "Dining Philosophers" synchronization problem. It serves as an introduction to the basics of threading a process.

This project introduces important concepts such as:
- Multithreading and process management using `pthread`
- Shared memory synchronization using Mutexes (`pthread_mutex`)
- Preventing deadlocks and data races
- Creating an external monitor routine to track thread states in real-time
- Strict memory management to avoid leaks and handle clean process exits

## 🚀 Instructions

Compile the project using the provided Makefile:
`make`

To execute the program, run the executable with the required arguments:
`./philo number_of_philosophers time_to_die time_to_eat time_to_sleep [number_of_limit_meals]`

Example (no philosopher should die):
`./philo 5 800 200 200`

Example with the optional argument (simulation stops when all philosophers have eaten 7 times):
`./philo 5 800 200 200 7`

## 📚 Resources

- Multithreading in C (Unix Threads) Playlist: https://www.youtube.com/watch?v=zOpzGHwJ3MU
- Introduction to Threads (pthread_create): https://www.youtube.com/watch?v=VSkvwzqo-Pk
- AI (Gemini) was used as an interactive tutor for conceptual clarification (multithreading, data races, monitor routine logic) and the structuration of this README.md file.

## ⚙️ Usage & Arguments

Here is the breakdown of the arguments required to run the simulation:

| Argument | Description |
|:---|:---|
| `number_of_philosophers` | The number of philosophers and forks around the table. |
| `time_to_die` (in ms) | Time a philosopher can survive without starting a new meal. |
| `time_to_eat` (in ms) | Time it takes for a philosopher to eat (requires 2 forks). |
| `time_to_sleep` (in ms) | Time a philosopher spends sleeping after eating. |
| `[number_of_limit_meals]` | The simulation stops if all philosophers have eaten at least this many times. |

## Thread
A thread is the smallest sequence of programmed instructions that can be managed independently by an operating system.

    Resource sharing: Unlike traditional processes (created via fork) which each have their own isolated memory space, all threads created within the same program share the exact same global memory.

    Parallelism: They allow a program to perform multiple tasks "at the same time." In your project, each philosopher is a separate thread: they all execute the same function (philo_routine) but progress at their own pace asynchronously.

## Mutex (Mutual Exclusion)
A mutex is a synchronization mechanism (a lock) that prevents multiple threads from accessing the same shared resource simultaneously, thereby avoiding memory corruption known as data races.

    The lock principle: When a thread needs to read or write critical data (like the time of a meal or the state of a fork), it engages the lock using pthread_mutex_lock.

    The waiting queue: If another thread tries to lock this already-locked mutex, the processor immediately pauses it. This second thread will remain frozen until the first one releases the lock with pthread_mutex_unlock.

    Security guarantee: The mutex ensures that a specific block of code or a variable is only manipulated by one single thread at any given moment.
