# University Timetable Optimizer - Benchmark Data

This directory contains standard CSV datasets for testing and benchmarking timetable scheduling algorithms (Greedy Baseline vs Genetic Algorithm).

## Schema Definitions

### 1. `courses.csv`
Represents individual course lecture or lab sections that must be scheduled.
| Column | Type | Description |
|---|---|---|
| `course_id` | String | Unique course code (e.g., `CS101`, `CS202`) |
| `course_name` | String | Title of the subject |
| `cohort_id` | String | Cohort / student section that attends this course |
| `faculty_id` | String | Assigned faculty member |
| `credits` | Integer | Course credit hours (number of 1-hour sessions needed per week) |
| `requires_lab` | Boolean | `true` if course must be scheduled in a specialized lab room |

### 2. `rooms.csv`
Represents classrooms, lecture halls, and laboratories.
| Column | Type | Description |
|---|---|---|
| `room_id` | String | Unique identifier (e.g., `R101`, `LAB201`) |
| `room_name` | String | Human readable room name |
| `capacity` | Integer | Maximum seating capacity |
| `is_lab` | Boolean | `true` if room is equipped with lab hardware / computers |
| `building` | String | Campus building location |

### 3. `faculty.csv`
Represents teaching faculty members and their scheduling constraints.
| Column | Type | Description |
|---|---|---|
| `faculty_id` | String | Unique instructor ID (e.g., `F01`, `F02`) |
| `name` | String | Faculty member's full name |
| `department` | String | Department affiliation |
| `max_hours_per_week` | Integer | Maximum teaching load allowed |
| `available_days` | String | Semicolon-delimited list of available days (e.g., `Mon;Tue;Wed;Thu;Fri`) |

### 4. `cohorts.csv`
Represents student cohorts (e.g., sections/batches of students who take courses together).
| Column | Type | Description |
|---|---|---|
| `cohort_id` | String | Unique cohort ID (e.g., `CSE-A`, `CSE-B`) |
| `cohort_name` | String | Display name for the student cohort |
| `size` | Integer | Total number of students in the cohort |
| `department` | String | Department (e.g., `Computer Science`) |

### 5. `timeslots.csv`
Represents weekly scheduling slots across standard university teaching hours.
| Column | Type | Description |
|---|---|---|
| `timeslot_id` | String | Unique timeslot key (e.g., `MON_09_10`, `TUE_14_15`) |
| `day` | String | Day of week (`Mon`, `Tue`, `Wed`, `Thu`, `Fri`) |
| `start_time` | String | Start time (`09:00`, `10:00`, etc.) |
| `end_time` | String | End time (`10:00`, `11:00`, etc.) |
| `slot_index` | Integer | Linear sequential index (0 to 24) |
