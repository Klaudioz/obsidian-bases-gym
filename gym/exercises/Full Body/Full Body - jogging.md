---
exercise-name: Full Body - jogging
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Full Body
weight: 0
reps: 1
sets: <% await tp.system.prompt("Sets", "3", true) %>
duration: <% await tp.system.prompt("Duration (seconds)", "3600", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Full Body
equipment: Bodyweight
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: 'jogging.'
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```