A single-file, hands-on practice lab for web accessibility. It covers keyboard and screen reader patterns, contrast and magnification testing, an automated scanner, a broken-versus-fixed UI workshop, and an audit checklist that exports a report. It targets WCAG 2.1 AA, with a few WCAG 2.2 success criteria added.

There is no build step, no framework and no dependencies. Open `a11y-lab-advanced.html` in a browser and it works.

## Quick start

1. Download `a11y-lab-advanced.html`.
2. Open it in any modern browser (Chrome, Edge, Firefox, Safari).
3. Work through the four modules from the tab bar.

The only external request is the Atkinson Hyperlegible font from Google Fonts. Offline, the page falls back to the system font and everything else still works.

## Modules

### 1. Keyboard and ARIA
Working examples of common widgets, each with what to test and which ARIA it uses:

- Tabs (roving tabindex; Left, Right, Home, End)
- Accordion (`aria-expanded`, `aria-controls`)
- Modal dialog (native `<dialog>` with `showModal()`, focus returns on close)
- Menu button (Enter or Down opens; arrows, Home, End move; Esc closes)
- Form validation (error summary receives focus, links jump to fields, status announced via `role="status"`)
- Live keyboard event log that shows each key and the focused element, for checking focus order

### 2. Contrast and zoom
- **Contrast checker** using the WCAG relative luminance formula. Reports AA and AAA results for normal text, large text and UI components, plus a grade badge. Includes a swap button and suggestions for a passing text color at 4.5:1 or 7:1 that keep the original hue.
- **Magnification tester** with text size from 100% to 400%, a 320px reflow simulation (SC 1.4.10), a text spacing simulation (SC 1.4.12) and color vision filters (protanopia, deuteranopia, tritanopia, achromatopsia). It warns when content scrolls horizontally.

### 3. Fix the UI
A small shop page in two versions, "Before" with 14 deliberate failures and "After" with each one fixed. Switch between Before, After and side by side.

- **Automated scanner**: runs DOM checks on both versions. It looks for missing alt text, buttons without an accessible name, click handlers on non-interactive elements, inputs without labels, positive tabindex, tables without header cells, vague link text and skipped heading levels.
- **Issue tracker**: 14 issue cards, each with the success criterion, level, who is affected, how to detect it, the fix, and before and after code. Tick Found and Fixed to track progress, and filter by Level A, Level AA or not yet found.

### 4. Audit report
A checklist of 21 success criteria grouped by Perceivable, Operable, Understandable and Robust. Mark each Pass, Fail or Not applicable and add notes. A live summary shows pass, fail, not rated and pass rate.

The report can be copied as text, downloaded as `.txt` or `.json`, or printed.

## Themes
Light, Dark and High contrast, selectable from the header. The first visit follows your operating system preference. All colors are CSS custom properties defined at the top of the stylesheet.

## Saved data
Progress is stored in your browser's `localStorage` under keys starting with `a11ylab.`:

| Key | Contents |
| --- | --- |
| `theme` | Selected theme |
| `tab` | Last open module |
| `iss` | Found and Fixed ticks in the issue tracker |
| `ck` | Checklist results and notes |

Nothing is sent anywhere. Use "Reset all progress" in the header to clear everything. If storage is blocked, the app still works but does not remember anything.

## Customizing

| To change | Edit |
| --- | --- |
| Colors for a theme | The `:root` and `:root[data-theme=...]` blocks |
| Issues in the workshop | The `IS` array (name, SC number, title, level, who is affected, how to detect, fix, before code, after code) |
| Sample page | The `sample()` function. If you change the number of issues, update `max` on the `#pbar` progress element |
| Checklist items | The `CK` array (principle, SC number, name) |
| Scanner rules | The `scanRoot()` function |

## Accessibility features of the app itself
- Skip link, landmarks, `lang` attribute and a logical heading structure
- Visible focus on every interactive element
- Touch targets of at least 44px
- Errors shown as text, not color alone
- Respects `prefers-reduced-motion`
- Reflows on small screens, with the tab bar scrolling sideways
- Print styles that hide the controls

## Limitations
- The scanner, contrast checker and simulations only check what can be computed. Automated tools cover only part of WCAG, so keep testing manually.
- The magnification and color vision tools are simulations. Also test with browser zoom, the OS magnifier and real assistive technology such as NVDA, JAWS, VoiceOver or TalkBack.
- The "Before" sample contains a deliberate keyboard trap. Press Esc to leave it.
- Skipped heading levels are strictly a best practice unless they misrepresent the structure, as noted in the issue card.
- This README describes the file as delivered. It has not been tested across every browser and screen reader combination.

## Files

| File | Purpose |
| --- | --- |
| `a11y-lab-advanced.html` | The whole app: markup, styles and scripts |
| `README.md` | This document |
