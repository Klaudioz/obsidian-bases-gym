<%*
// Step 1: Select muscle group
const muscleGroup = await tp.system.suggester(
  ["Abs", "Biceps", "Calves", "Chest", "Core", "Forearms", "Front Deltoids", "Full Body", "Glutes", "Hamstrings", "Lateral Deltoids", "Lats", "Lower Back", "Lower Body", "Neck", "Rear Deltoids", "Rotator Cuff", "Shoulders", "Traps", "Triceps", "Upper Body"],
  ["Abs", "Biceps", "Calves", "Chest", "Core", "Forearms", "Front Deltoids", "Full Body", "Glutes", "Hamstrings", "Lateral Deltoids", "Lats", "Lower Back", "Lower Body", "Neck", "Rear Deltoids", "Rotator Cuff", "Shoulders", "Traps", "Triceps", "Upper Body"]
);

// Step 2: Show exercises for that muscle group
const exercisesByGroup = {
  "Abs": ["Abs - leg raises"],
  "Biceps": ["Biceps - dumbbells hammer curl"],
  "Calves": ["Calves - seated calf raises", "Calves - single leg calf raises"],
  "Chest": ["Chest - chest fly", "Chest - decline push up", "Chest - dumbells floor press"],
  "Core": ["Core - plank"],
  "Forearms": ["Forearms - dumbell finger curl", "Forearms - farmer's walk"],
  "Front Deltoids": ["Front Deltoids - dumbbells front raise"],
  "Full Body": ["Full Body - jogging"],
  "Glutes": ["Glutes - glute bridge", "Glutes - hip thrust"],
  "Hamstrings": ["Hamstrings - dumbells romanain deadlift"],
  "Lateral Deltoids": ["Lateral Deltoids - lateral raise"],
  "Lats": ["Lats - pull up", "Lats - seated dumbbell row"],
  "Lower Back": ["Lower Back - superman"],
  "Lower Body": ["Lower Body - jump squat", "Lower Body - pistol squat", "Lower Body - squat"],
  "Neck": ["Neck - neck bridge", "Neck - neck curl"],
  "Rear Deltoids": ["Rear Deltoids - reverse fly"],
  "Rotator Cuff": ["Rotator Cuff - dumbells cuban press"],
  "Shoulders": ["Shoulders - pike push up"],
  "Traps": ["Traps - dumbells shrug"],
  "Triceps": ["Triceps - dips", "Triceps - dumbbell kickback", "Triceps - dumbbells skull crusher"],
  "Upper Body": ["Upper Body - dumbells overhead press", "Upper Body - push up"]
};

const exerciseName = await tp.system.suggester(exercisesByGroup[muscleGroup], exercisesByGroup[muscleGroup]);

// Step 3: Determine workout type
let workoutType = "Upper Body Push";
if (["Biceps", "Lats"].includes(muscleGroup)) workoutType = "Upper Body Pull";
if (["Rear Deltoids"].includes(muscleGroup)) workoutType = "Upper Body Pull";
if (["Lower Body", "Glutes", "Hamstrings", "Calves"].includes(muscleGroup)) workoutType = "Lower Body";
if (["Abs", "Core", "Lower Back"].includes(muscleGroup)) workoutType = "Core";
if (["Full Body"].includes(muscleGroup)) workoutType = "Full Body";
if (["Neck", "Traps", "Forearms", "Rotator Cuff"].includes(muscleGroup)) workoutType = muscleGroup;

// Step 4: Prompt for workout details
const weight = await tp.system.prompt("Weight (lbs) - enter 0 for bodyweight", "0");
const reps = await tp.system.prompt("Reps", "10");
const sets = await tp.system.prompt("Sets", "3");
const effort = await tp.system.suggester(["1 (easy)", "2", "3", "4", "5 (failure)"], ["1", "2", "3", "4", "5"]);
const notes = await tp.system.prompt("Notes (optional)", "");

// Step 5: Auto-rename and move file
const date = tp.date.now("YYYY-MM-DD");
await tp.file.move(`gym/Log/${date} ${exerciseName}`);
-%>
---
exercise-name: <% exerciseName %>
exercise-date: <% tp.date.now("YYYY-MM-DD") %>
muscle-group: <% muscleGroup %>
weight: <% weight %>
reps: <% reps %>
sets: <% sets %>
effort: <% effort %>
workout-type: <% workoutType %>
notes: "<% notes %>"
---

# Workout Log - <% tp.date.now("MMMM DD, YYYY") %>

## Performance Notes
Add your notes here about form, how it felt, etc.

## Next Session
- Consider increasing weight, reps, or sets
- Focus on maintaining proper form

---

**✅ This workout has been automatically saved to `gym/Log/` and will appear in your dashboard!**
