---
exercise-name: Core - plank
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Core
weight: 0
reps: 1
sets: <% await tp.system.prompt("Sets (number of holds)", "3", true) %>
duration: <% await tp.system.prompt("Duration per set (seconds)", "45", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Core
equipment: Bodyweight
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: 'plank, hold it.'
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```