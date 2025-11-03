
Your complete workout tracking and performance overview.

---

## Recent Exercises

All workouts sorted by date. **Click the exercise-date column header to sort newest first.**

```base
filters:
  and:
    - file.inFolder("gym/Log")
views:
  - type: table
    name: Recent Workouts
    order:
      - exercise-date
      - exercise-name
      - muscle-group
      - sets
      - reps
      - weight
      - effort
    sort:
      - property: exercise-date
        direction: DESC

```

---

## High Effort Training

Workouts with maximum effort (4-5/5). These are your challenging, rewarding sessions.

```base
filters:
  and:
    - file.inFolder("gym/Log")
    - effort >= 4

views:
  - type: table
    name: "High Effort Sessions"
    order:
      - exercise-date
      - exercise-name
      - muscle-group
      - weight
      - sets
      - reps
      - effort
```

---

## Exercises by Muscle Group

View all logged exercises organized by the muscle groups they target.

```base
filters:
  and:
    - file.inFolder("gym/Log")

views:
  - type: table
    name: "By Muscle Group"
    order:
      - muscle-group
      - exercise-date
      - exercise-name
      - weight
      - reps
      - sets
```

---

## All Exercise History

Complete history of all logged workouts. Use this to track your progression over time.

```base
filters:
  and:
    - file.inFolder("gym/Log")

views:
  - type: table
    name: All Exercises
    order:
      - exercise-date
      - exercise-name
      - muscle-group
      - weight
      - reps
      - sets
      - effort
```


---

## Quick Links

- **[Upper Body Push Routine](routines/Upper%20Body%20Push.md)** - Use as template for push days
- **[Lower Body Routine](routines/Lower%20Body.md)** - Use as template for leg days

---

## How to Log a New Exercise

1. Create a new markdown file in the `gym/Log/` folder
2. Use naming convention: `YYYY-MM-DD ExerciseName.md` (e.g., `2025-10-30 Bench Press.md`)
3. Copy the YAML frontmatter from a sample exercise file
4. Update these properties:
   - `exercise-name`: Name of the exercise
   - `exercise-date`: Date you performed it (YYYY-MM-DD)
   - `muscle-group`: Primary muscle group (Chest, Back, Legs, Shoulders, Arms, etc.)
   - `weight`: Weight used in pounds (0 for bodyweight)
   - `reps`: Number of repetitions
   - `sets`: Number of sets
   - `effort`: Effort level 1-5 (1=easy, 5=max effort)
   - `workout-type`: Type of workout (Upper Body Push, Lower Body, etc.)
   - `notes`: Any observations about form or performance

4. Optionally add markdown notes below the frontmatter
5. The new exercise will automatically appear in all relevant views

---

## Tips for Success

- **Be consistent**: Log every session to build accurate data
- **Track progression**: Notice patterns in weight, reps, and effort
- **Use the routines**: Templates provide structure to your training
- **Add notes**: Your observations help identify what works best
- **Review weekly**: Look at the weekly view to assess volume and balance

---

Last dashboard update: Today's date
