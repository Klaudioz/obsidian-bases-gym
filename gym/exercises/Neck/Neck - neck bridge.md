---
exercise-name: Neck - neck bridge
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: Neck
weight: 0
reps: <% await tp.system.prompt("Reps", "20", true) %>
sets: <% await tp.system.prompt("Sets", "3", true) %>
effort: <% await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]) %>
workout-type: Neck
equipment: Bodyweight
notes: <% await tp.system.prompt("Notes", "", true) %>
instructions: 'do isometric. avoid using your top part of your head.'
tags:
  - exercise
---

```dataviewjs
const {exercise} = customJS;
const note = {dv: dv, container: this.container, window: window};

exercise.renderDescription(note);
exercise.renderEffortWeightChart(note);
```