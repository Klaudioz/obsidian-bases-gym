# Obsidian Gym Tracker

A lightweight workout tracking system for [Obsidian](https://obsidian.md/), built with Obsidian Bases. Track exercises, monitor progress, and visualize training data. All data stored as markdown files with YAML frontmatter. Inspired by [martinjo's obsidian-gym-log](https://github.com/martinjo/obsidian-gym-log).

## Features

- Native Obsidian Bases integration (no plugin dependencies)
- Simple markdown files with YAML frontmatter
- Automatic calculations for volume, intensity scores, progress metrics
- Multiple views by date, muscle group, exercise type, effort level
- Exercise library with 33+ templates across 22 muscle groups
- Pre-built workout routine guides
- Data visualization with effort and volume metrics
- Progress tracking with chronological logs

## Prerequisites

- Obsidian v1.10.0 or later (required for Bases feature)
- A local Obsidian vault

## Installation

This tracker is configured to work in a `gym/` subfolder in your vault.

### Step 1: Clone or Download

```bash
git clone <your-repo-url>
# OR download and extract the ZIP
```

### Step 2: Copy to Your Vault

Copy files in two steps:

**Step 2a: Copy the gym folder**
```
FROM: gym/                        TO: YourVault/gym/
```

**Step 2b: Copy the Gym.base file**
```
FROM: gym/Bases/Gym.base          TO: YourVault/Bases/Gym.base
```

**Your vault structure should be:**

```
YourVault/
├── Bases/                        ← Vault-level bases folder
│   ├── Gym.base                  ← Database configuration (MUST be here!)
│   └── [other .base files]
├── gym/                          ← Your gym tracking folder
│   ├── Bases/
│   │   └── Gym.base              ← Copy for GitHub, but Obsidian uses /Bases/Gym.base
│   ├── Log/                      ← Your workout logs go here
│   ├── exercises/                ← Exercise templates (reference)
│   ├── routines/                 ← Workout planning guides
│   ├── Gym Dashboard.md          ← Open this to view your data
│   └── README.md
├── [your other vault files]
└── ...
```

**Why This Structure?**

- Obsidian Bases convention: `.base` files MUST go in vault's `Bases/` folder (not in subfolders)
- The configuration uses `file.inFolder("gym/Log")` which looks for files in the `gym/` subfolder
- You MUST keep the `gym/` folder name. Renaming it will break the tracker
- If you want a different folder name, update all paths in `Bases/Gym.base` and `Gym Dashboard.md`

### Step 3: Verify Installation

1. Restart Obsidian
2. Open `gym/Gym Dashboard.md`
3. You should see 3 sample workouts from 2025-10-30
4. If you see "0 results", jump to Troubleshooting section below

## Quick Start

### View Your Dashboard

Open `gym/Gym Dashboard.md` to see:
- Recent Workouts: All logged workouts sorted by date
- High Effort Training: Workouts with effort level 4-5
- Exercises by Muscle Group: All workouts organized by muscle
- All Exercise History: Complete chronological log

Note: Date filtering (Today, This Week, etc.) is not supported in dashboard inline queries. For date-filtered views, open the Gym base directly from Obsidian's Bases section in the sidebar.

### Log Your First Workout

1. Navigate to the `gym/Log/` folder
2. Create a new markdown file: `YYYY-MM-DD ExerciseName.md`
   - Example: `2025-10-30 Deadlift.md`
3. Add this YAML frontmatter:

```yaml
---
exercise-name: Deadlift
exercise-date: 2025-10-30
muscle-group: Back
weight: 315
reps: 5
sets: 3
effort: 4
workout-type: Lower Body
notes: "Strong pulls, good form throughout"
---

# Deadlift - 2025-10-30

Great session today. Form felt solid on all sets.
```

4. Save the file
5. Reload the dashboard (Ctrl/Cmd + R)
6. Your workout appears in all relevant views

### Find Exercise Names

Browse the `gym/exercises/` folder to find exercises by muscle group. Copy the exact exercise name from the template to use in your logs.

### Access Date-Filtered Views

The Gym base file includes date-filtered views. To access them:

1. Open Obsidian
2. Look in the left sidebar for the Bases section (or search for "Gym")
3. Click on Gym base
4. You'll see these views with working date filters:
   - Today's Workout: Exercises from today only
   - This Week: Last 7 days of training
   - Recent 30 Days: Last month's workouts
   - Personal Records: High-effort sessions (4-5)
   - All Exercises: Complete history
   - By Muscle Group: Organized by muscle

Why the difference? Obsidian Bases support date filtering (`today()`, date arithmetic) in `.base` files, but these functions don't work in inline dashboard queries. The dashboard shows all workouts and filtered views, while the base file provides date-specific filtering.

## Properties Reference

Every workout log uses these properties:

| Property | Type | Example | Description |
|----------|------|---------|-------------|
| `exercise-name` | text | "Bench Press" | Name of the exercise |
| `exercise-date` | date | 2025-10-30 | Date performed (YYYY-MM-DD) |
| `muscle-group` | text | "Chest" | Primary muscle targeted |
| `weight` | number | 225 | Weight in pounds (use 0 for bodyweight) |
| `reps` | number | 8 | Repetitions per set |
| `sets` | number | 4 | Number of sets |
| `effort` | number | 4 | Effort level 1-5 (1=easy, 5=all-out) |
| `workout-type` | text | "Upper Body Push" | Category of workout |
| `notes` | text | "Great session" | Optional observations |

## Automatic Formulas

The system calculates these metrics automatically:

- **volume** = weight × reps × sets (total mechanical work)
- **intensity_score** = (effort / 5) × (weight × reps) (effort-weighted metric)
- **days_since_exercise** = days elapsed since the exercise
- **total_sets** = number of sets completed

These appear in dashboard views and can be used for filtering and sorting.

## Using the Exercise Library

The `exercises/` folder contains 33+ templates organized by 22 muscle groups:

Abs, Biceps, Calves, Chest, Core, Forearms, Front Deltoids, Full Body, Glutes, Hamstrings, Lateral Deltoids, Lats, Lower Back, Lower Body, Neck, Rear Deltoids, Rotator Cuff, Shoulders, Traps, Triceps, Upper Body

These templates are for reference. Use them to find correct exercise names and see example formats.

## Workout Routines

The `routines/` folder contains comprehensive guides:

- Training Splits.md: 5 different training split approaches
- Upper Body Push.md: Structured push day routines
- Lower Body.md: Leg day programming
- Pull Day.md: Pull/back day routines

Review these to plan your training structure.

## Troubleshooting

### Dashboard Shows "0 Results"

Most Common Cause: Gym.base file is not in the correct location.

Solutions:

1. Verify Gym.base location (MOST IMPORTANT):
   - `Gym.base` MUST be at `/Bases/Gym.base` (vault root, not in gym/ folder)
   - Obsidian ignores `.base` files in subfolders
   - If you only copied the gym/ folder, you missed this step
   - Copy `gym/Bases/Gym.base` → `YourVault/Bases/Gym.base`

2. Verify folder locations:
   - Workout logs must be in `gym/Log/` folder
   - The folder MUST be named `gym/` exactly
   - Check by looking at your vault's file tree in Obsidian

3. Check Obsidian version:
   - Bases requires v1.10.0 or later
   - Go to Settings → About to check version
   - Update via Help → Check for updates if needed

4. Reload Obsidian:
   - Close and reopen Obsidian completely
   - Or use Ctrl/Cmd + R to reload
   - Bases views sometimes need a refresh

5. Verify YAML format:
   - Frontmatter must start and end with `---`
   - Property names must match exactly: `exercise-name`, `exercise-date`, `muscle-group`
   - Numbers should NOT have quotes: `weight: 225` (correct) vs `weight: "225"` (wrong)

6. Check file names:
   - All workout logs must be `.md` files
   - Must be in the `gym/Log/` folder

### Properties Not Showing

- Verify property names use hyphens: `exercise-name` not `exercise_name` or `exerciseName`
- Property names are case-sensitive
- Ensure YAML frontmatter is properly formatted

### Formulas Not Calculating

- All required properties must have values (weight, reps, sets, effort)
- Numbers must not have quotes
- Check that formulas are defined in `Gym.base`

### Dates Not Working

- Use YYYY-MM-DD format only
- Example: `2025-10-30` (correct)
- NOT: `10/30/2025` or `10-30-2025` (wrong)

### Still Not Working?

Create a test file to diagnose:

1. Create `gym/Log/2025-10-30 Test.md`
2. Add minimal frontmatter:

```yaml
---
exercise-name: Test
exercise-date: 2025-10-30
muscle-group: Chest
weight: 100
reps: 10
sets: 3
effort: 3
workout-type: Test
notes: ""
---
```

3. Save and reload dashboard
4. If this appears, the issue is with your other files' formatting
5. If not, verify your installation follows the structure above exactly

## Customization

### Add New Views

Edit `Bases/Gym.base` and add a view block:

```yaml
- type: table
  name: "Heavy Lifts"
  filters:
    and:
      - file.inFolder("Log")
      - weight >= 200
  order:
    - exercise-date
    - weight
```

### Add New Properties

Add to the `properties:` section in `Gym.base`:

```yaml
properties:
  body-weight:
    displayName: "Body Weight"
```

Then add it to workout logs in YAML frontmatter.

### Modify Formulas

Edit the `formulas:` section in `Gym.base`:

```yaml
formulas:
  custom-metric: (weight * reps) / body-weight
```

See [Obsidian Bases documentation](https://help.obsidian.md/Bases/Introduction+to+Bases) for formula syntax.

## Tips & Best Practices

- Consistent naming: Use `YYYY-MM-DD ExerciseName.md` format for chronological sorting
- Log immediately: Record details right after workouts while fresh
- Use effort levels: The 1-5 scale helps identify your hardest sessions
- Add notes: Observations about form, fatigue, and mood are valuable
- Review weekly: Check dashboard trends to identify patterns
- Update routines: Keep routine templates synced with your current plan

## Exporting Data

All data is stored as markdown files:
- Copy files to backup
- Commit to Git for version history
- Export to CSV using Obsidian tools
- Process with external scripts
- Share individual workout logs easily

## Support & Resources

- Obsidian Bases Help: https://help.obsidian.md/Bases/Introduction+to+Bases
- Obsidian Forum: https://forum.obsidian.md
- Report Issues: Create an issue in this repository

## Contributing

Feel free to customize properties, formulas, and views for your needs. Share improvements with the community by submitting pull requests.

## License

This project is open source and available under the MIT License.

## Acknowledgments

- Original [obsidian-gym-log](https://github.com/martinjo/obsidian-gym-log) by martinjo
- Obsidian Community