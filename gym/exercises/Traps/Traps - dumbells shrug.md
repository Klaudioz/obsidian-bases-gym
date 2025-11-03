---
exercise-name: Traps - dumbells shrug
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Traps
weight: <% await tp.system.prompt("Weight (lbs)", "", true) %>
reps: <% await tp.system.prompt("Reps", "12", true) %>
sets: <% await tp.system.prompt("Sets", "3", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Traps
equipment: Pair of Dumbbells
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: 'shrug it off'
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```