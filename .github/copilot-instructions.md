# Copilot instructions

## Build, test, and lint

- There are no configured build, test, or lint commands. The app is a standalone `index.html`; open it directly in a browser (`file://`) to run it without a server or dependencies.
- For a browser smoke test, check answer selection and feedback, score and progress updates, moving through all 10 questions, the results screen, and the Play again reset.

## Architecture

- The app lives entirely in `index.html`: semantic page markup, inline CSS, the question data, and the quiz controller are in one file. There is no package manifest, framework, server, or external runtime dependency.
- The `questions` array is the source of truth for quiz content. `renderQuestion()` updates the current question and progress; `chooseAnswer()` locks choices, updates the score, and shows feedback; `showResults()` replaces the quiz card with the result view; `restart()` restores the quiz and rebinds its DOM references and event handlers.
- Styling and interaction behavior share this file: CSS custom properties define the light/dark palettes, while CSS media queries handle responsive layout and reduced motion.

## Code conventions

- Keep the app self-contained in `index.html`; do not introduce a build step or runtime dependency for ordinary quiz changes.
- Keep each question's category, prompt, choices, correct-choice index, and explanation together in its question object. The `answer` index refers to the corresponding entry in `options`.
- The results and restart views replace `#quiz` contents. When changing their markup, keep `restart()`'s element rebinding in sync with the initial quiz markup and attach handlers to the recreated controls.
- Preserve accessible native buttons, visible keyboard focus, focus handoff to Next after answering and to the heading on results/restart, live feedback, and progress-bar labels/values.
- Put colors in the existing CSS custom properties and update both the default and `prefers-color-scheme: dark` palettes. Respect `prefers-reduced-motion` for any new animation.
