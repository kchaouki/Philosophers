# Philosophers

A C implementation of the **Dining Philosophers** problem — a classic concurrency exercise from the [42 School](https://42.fr) curriculum.

## The Problem

A number of philosophers sit at a round table with a fork between each pair of adjacent philosophers. Each philosopher alternates between thinking, eating, and sleeping. To eat, a philosopher needs both the fork to their left and the fork to their right. The simulation ends when a philosopher dies of starvation or, optionally, when every philosopher has eaten a minimum number of times.

## Structure

```
Philosophers/
├── philo/          # Mandatory part — uses threads and mutexes
└── philo_bonus/    # Bonus part — uses processes and semaphores
```

### philo (mandatory)

Each philosopher is a **thread**. Forks are protected by **mutexes**.

### philo_bonus

Each philosopher is a **process**. Forks are managed via a **semaphore** pool.

## Usage

### Build

```bash
# Mandatory
cd philo && make

# Bonus
cd philo_bonus && make
```

### Run

```bash
./philo <number_of_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [number_of_times_each_philosopher_must_eat]
```

| Argument | Description |
|---|---|
| `number_of_philosophers` | Number of philosophers (and forks) |
| `time_to_die` (ms) | Time before a philosopher dies if they haven't started eating |
| `time_to_eat` (ms) | Time it takes to eat |
| `time_to_sleep` (ms) | Time spent sleeping |
| `number_of_times_each_philosopher_must_eat` | *(optional)* Stop when all philosophers have eaten this many times |

### Examples

```bash
# 5 philosophers, never die
./philo 5 800 200 200

# 4 philosophers, each must eat at least 7 times
./philo 4 410 200 200 7

# Edge case: single philosopher (can never eat — dies)
./philo 1 800 200 200
```

## Notes

- Timestamps are printed in milliseconds from the start of the simulation.
- No philosopher should die if the arguments are reasonable.
- There are no data races — all shared state is protected by mutexes (mandatory) or semaphores (bonus).

## Author

[kchaouki](https://github.com/karimch-50) — student at 1337 (42 Network)
