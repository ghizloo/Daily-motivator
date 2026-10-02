# Project history

Notes written in early October 2026 from the chat sessions that produced this project. It is a summary, not a transcript.

## Why this exists

The owner wanted to organize cooking, studying, a hobby and workouts around three real constraints: energy level, sleep quality, and a work schedule that is partly fixed and partly decided by shift coverage requests. Earlier attempts at plans did not stick because they ignored energy and sleep.

## Timeline

1. **First version.** A single page, "Your Week, By Energy", built as a Claude artifact. The owner picks Low, Medium or High energy for each day and says whether they are covering Friday or Monday. The page rotated workout, study, cooking and hobby suggestions around free time. Nothing demanding was placed before 9am because mornings are hard.
2. **Visual direction.** The first dark look felt gloomy. It became a warm paper look with a playful italic headline, rounded body type, and a color per activity. Original cartoon animal mascots were added per activity (bunny, owl, chef cat, panda, later turtle, fox, koala). The owner called it "super cute".
3. **Syncing across devices.** The owner uses a work desktop, a personal laptop and a phone. Syncing through the artifact platform's shared storage was tried. After that, buttons stopped responding in the in-chat preview. Removing the sync feature fixed it, so the cause was most likely that feature, though it was never fully proven. Browser-only storage was used from then on. GitHub Pages is static hosting, so cross-device sync still needs a real solution (see roadmap).
4. **Dashes.** The owner noticed dashed borders and dash characters in text and said it looks AI made. Dashed borders, em dashes and en dashes were removed, and this became a standing design rule.
5. **Per-energy plans.** Workouts and study were given real content for Low, Medium and High, tied to weekdays: lower body on Friday, upper body and posture on Sunday, a short light session on Monday after a Pilates class, light stretching on Tuesday and Thursday, Wednesday only if energy is High, Saturday as rest. Study got three types: thorough (Monday, Friday, Sunday), super light (Tuesday, Thursday), and conditional (Wednesday and Saturday). The rule that study cannot be skipped on free days came from a hard certification deadline. Exercise lists are not stored here on purpose (public repo).
6. **A build that went wrong.** One large update added checkboxes, a theme panel with dark mode and a custom color picker, and more animals. The owner reported that existing content had disappeared, the colors did not match, and the color picker did not work. Headless tests had passed. The owner stopped the work and asked to rebuild as an app together, one step at a time, creating nothing until told.
7. **App direction.** The goal became a real app with daily plans, habits, streaks, mood check-ins and affirmations. Chosen path: perfect the idea as an HTML prototype first. A real iPhone app with Apple Health and Apple Watch support needs a native Swift app and is a separate, later project.
8. **Repository.** The owner published the site on GitHub (this repo). The `index.html` here is a larger single-file build than the early artifact: theme studio with 10 palettes plus custom accent and dark mode, week, day and month views, morning and evening moods, a night-before planner, a life library of habits and plans, affirmations, and emoji animals. Its authoring session is not documented in these notes.

## Decisions and why

- **Energy scales intensity, not just whether something happens.** Low energy is a smaller version of the day, not a skipped day. The exception is certification study on free days, which can shrink but not vanish.
- **Local storage only, for now.** Simple and private. Costs: no cross-device sync, and data is lost if browser data is cleared. Export and import of a JSON file is the cheapest next step.
- **Single file, no build step.** Easy for a non-developer to host and for agents to edit. Revisit if the file gets unmanageable.
- **Cooking and diet in a separate PDF.** The owner decided cooking detail should not live in the app for now.
- **Inspiration, not imitation.** Two App Store apps (Me + Lifestyle routine, Structured) set the bar for structure. The owner wants more detail and an original look.

## Lessons

- Big multi-feature rewrites broke a working page. Ship one change at a time.
- Headless tests are necessary but not enough. The owner's real browser showed failures the tests did not.
- Adding a platform-specific feature (shared storage) to a page that worked fixed nothing and broke it. Test such features in the real target environment first.
- The owner's stated preferences (no dashes, cute animals, lively color) are requirements, not suggestions. Re-check every new screen against them.
