---
exercise-name: Lower Body - squat
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Lower Body
weight: <% await tp.system.prompt("Weight (lbs)", "", true) %>
reps: <% await tp.system.prompt("Reps", "12", true) %>
sets: <% await tp.system.prompt("Sets", "3", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Lower Body
equipment: Barbell
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: just squat.
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```