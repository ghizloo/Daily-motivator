# AGENTS.md

Orientation for any AI agent or developer picking up this project. Read this first, then `docs/HISTORY.md` and `docs/ROADMAP.md`.

## What this is

Weekly Rhythm (repo name: Daily-motivator) is a gentle planner, habit tracker and mood check-in that plans around the energy the user actually has. It is one static file, `index.html`: vanilla HTML, CSS and JS, no build step, no dependencies. Data lives in localStorage on a single device. The owner wants to grow it into a real app, starting with this HTML prototype.

## How to work with the owner

- The owner is not a developer. Explain in plain language, one idea at a time, and ask at most one question per message.
- Work one step at a time. An earlier attempt to add seven features in one go broke a working page and cost the owner's trust. Build one feature, test it, show it, then ask what is next.
- If the owner says to wait, do not create or change anything until they say go.
- Never remove or replace working features while adding new ones. Prefer small edits to `index.html` over regenerating the whole file.
- Say plainly what is not possible. Example: a web page cannot read Apple Health or Apple Watch data, that needs a native iOS app.
- Ask before large rewrites or redesigns.

## Design rules from the owner

- Lively, cute, colorful and warm. Not dark and gloomy. Light and dark modes are both wanted.
- Lots of cute animal characters, and not only next to tasks (headers, empty states, moods, celebrations). Prefer drawn SVG animals and faces over system emoji.
- No dashes in visible copy: no em dashes, no en dashes, no dashed borders. Use commas, periods or the word "to" for ranges. Also avoid middle dot separators and ALL CAPS labels, which make the app feel machine made.
- All color and theme controls live in one collapsible panel. Support preset themes, dark mode, and a custom accent color that really recolors the whole app. Colors must match each other in every theme and in dark mode.
- Do not copy any existing app. Inspiration only: Me + Lifestyle routine and Structured (App Store). Do not copy the InnerGrow "Habit Tracker" app.
- The mood scale is fixed: Excellent, Great, Good, Neutral, Poor, Bad, Awful. Each has a colorful face.

## Product rules

- Energy (Low, Medium, High) and mood decide what the day asks of the user. Lower energy means fewer and gentler tasks, never a failed day.
- Study for the owner's professional certification must not be skippable on free days, even at Low energy. It can shrink to a short session. On fixed work days, Low energy may skip it.
- Streaks matter for motivation. Not built yet.
- Each day has two sections: daily plans and habits.
- Cooking and diet detail will live in a separate PDF for now, not in this app.
- Workout plans scale by energy: High is the full session, Medium is the same session with one fewer set per exercise, Low is lighter weight and about two sets. Exercise lists are intentionally not stored in this public repo, ask the owner.

## Technical map of index.html

Written by reading the code. It has not been run in a browser as part of writing these notes.

- Layout: CSS in one `<style>` block, markup in the body, JS in one `<script>` at the bottom. Ends with `render(); generate();`.
- State: one object, `state`, saved by `save()` to localStorage key `weekly-rhythm-v2`. `load()` builds defaults. Main fields: `weekStart`, `bedtime`, `wake`, `coverMon`, `coverFri`, `targets` (study, workout, cook, hobby per week), `days` (keys Mon to Sun), `theme`, `dark`, `accent`, `view`, `library`, `selectedDay`.
- Per day (`state.days.Mon` etc.): `energy`, `sleep`, `work`, `note`, `moodStart`, `moodEnd`, `moodWhy`, `assigned`, `done`, `taskNotes`, `customTasks`, `tasks`, `fixedPlans`, `dailyMode`.
- Planning: `generate()` spreads the weekly targets across days using an energy and sleep score. `buildTomorrowTasks(day)` builds the night-before plan from `TASK_POOL` plus the user's library, filtered by energy and mood.
- Rendering: `render()` calls `renderWeek()`, `renderPriorities()`, `renderInsight()`, `renderLibrary()` and the view switcher `setView()` for week, day (`renderDayView()`) and month (`renderMonth()`). An edit modal (`openModal()`) holds work text, moods, custom tasks and the main task choice.
- Themes: `THEMES` has 10 palettes, each with light and dark arrays of 9 colors mapped to CSS variables `--bg`, `--surface`, `--surface2`, `--text`, `--muted`, `--line`, `--accent`, `--accent2`, `--pageGlow` by `applyTheme()`.
- Fixed weekly skeleton: the `FIXED` object hardcodes the owner's work shifts (Tuesday late shift, Wednesday and Thursday day shifts, Saturday day shift, Monday and Friday flexible with coverage toggles, Sunday open). Make this editable before sharing the app with other people.

## Known issues

Found by reading the code:

1. Day data is keyed by weekday name, not by calendar date. The month view repeats the same weekday data for every date, and nothing is remembered from week to week. Streaks, mood history and notes need date keyed data, for example `state.log['2026-10-05']`.
2. Date helpers use `toISOString()`, which is UTC. In western time zones, evenings can return tomorrow's date. Use local date formatting.
3. `generate()` uses `Math.random()` as a tie breaker and runs on every energy or sleep click, so the plan can reshuffle and overwrite assignments unexpectedly.
4. Task completion notes use `window.prompt()` from a document-level change listener, and find the day by card position. Replace with inline UI.
5. Copy still contains em dashes, en dashes, middle dots and uppercase labels, which break the design rules above.
6. Moods and animals are system emoji. The owner wants drawn, colorful faces and cute illustrated animals.
7. The mood check-in is inside the Edit day modal and Day view. The owner wants it as the opening screen.
8. Two sections per day (plans and habits) are not implemented. The life library has habit, minimize and plan types but they are not shown as two day sections.

## Testing

There is no test framework. Before handing anything to the owner:

- Load the page headless (for example jsdom with a real URL so localStorage works), click the energy buttons, checkboxes and theme controls, and confirm the page re-renders and nothing disappears.
- Check a phone sized viewport and both light and dark mode.
- Check one non-UTC time zone for date bugs.
- Search the visible text for em dashes, en dashes and dashed borders.
- A passing headless test is not proof the real page works. A past sync feature passed headless tests and still broke buttons for the owner. If the owner says something is broken, believe them and investigate.

## Privacy

The repository is public. Do not commit health details, employer names, personal names, exam dates or resume content. Keep personal specifics in the conversation, not in files.
