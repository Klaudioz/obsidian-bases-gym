---
exercise-name: Front Deltoids - dumbbells front raise
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Front Deltoids
weight: <% await tp.system.prompt("Weight (lbs)", "", true) %>
reps: <% await tp.system.prompt("Reps", "8", true) %>
sets: <% await tp.system.prompt("Sets", "3", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Upper Body Push
equipment: Pair of Dumbbells
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: front
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```