# Roadmap

Agreed with the owner. Build one step at a time and get a thumbs up before starting the next. Do not start a step the owner has not approved.

## Agreed design

- The app opens with "How are you feeling?" showing seven colorful faces: Excellent, Great, Good, Neutral, Poor, Bad, Awful.
- After picking, the person can add a note about why, or skip the note.
- Then the day view shows what is ahead, shaped by the day's energy.
- Each day has two sections: daily plans, and habits.
- People can add their own plans and habits.
- Streak tracking keeps people motivated.
- The owner is thinking of this as something other people (clients) could use, so avoid hardcoding one person's life.

## Steps

1. **Opening mood screen.** Seven drawn, colorful faces, optional note, skip, saved by calendar date. Replace the emoji moods.
2. **Energy question and day view.** Ask for energy (Low, Medium, High) after mood. Show the day with two sections, daily plans and habits, adjusted to energy.
3. **Add and edit plans and habits.** Simple forms. The owner does not want a separate "one-off" concept, only the two sections per day.
4. **Streaks.** Per habit, based on date keyed history. This requires fixing known issue 1 in `AGENTS.md` first.
5. **Day, week and month views.** Overview in week and month, details only inside a day. Checking off a task offers an optional note, using inline UI instead of `window.prompt()`.
6. **End of day check-in.** Mood again, with an optional why.
7. **Daily affirmations.** Suggested by a friend of the owner. Pair each with an animal.
8. **Visual pass.** Cute illustrated animals throughout, consistent themes and dark mode, a working custom accent color, all color controls in one collapsible panel, no dashes anywhere.

## Later

- **Backup and cross-device use.** Start with export and import of a JSON file. Real sync needs a backend or an account system.
- **Make the weekly skeleton editable.** Work shifts are hardcoded in `FIXED`.
- **Native iPhone app.** SwiftUI with HealthKit and Apple Watch support. A separate project, because web pages cannot read Apple Health or Apple Watch data. Do iPhone first, Android later.
- **Cooking and diet PDF.** Separate document, not part of the app for now.
