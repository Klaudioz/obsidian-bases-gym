---
exercise-name: Lower Body - jump squat
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Lower Body
weight: 0
reps: <% await tp.system.prompt("Reps", "15", true) %>
sets: <% await tp.system.prompt("Sets", "3", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Lower Body
equipment: Bodyweight
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: 'jump'
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```