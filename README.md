# Full-Stack From Zero Roadmap

**Live website:** [https://anujbarwal.github.io/Full-Stack-From-Zero-Roadmap/](https://anujbarwal.github.io/Full-Stack-From-Zero-Roadmap/)

A responsive, beginner-friendly roadmap site for learning full-stack web development by building projects. It includes a searchable project ladder, a milestone tracker, a personal course countdown, an animated coding scene, and rotating quotations from computing history.

This is the standalone public copy of the website originally developed in [Anujbarwal/Anujbarwal](https://github.com/Anujbarwal/Anujbarwal). The original feature-by-feature pull request history is documented below.

The profile README now links back to this live site, its source, build guide, commit history, and all 15 feature PRs: [view the profile integration](https://github.com/Anujbarwal/Anujbarwal/pull/16) or its [merged commit](https://github.com/Anujbarwal/Anujbarwal/commit/743513b0186b77d547340db21874313bab25a99b).

## Build it step by step

### 1. Start with the smallest useful version

The site is a static website, so it does not need a server framework, database, package manager, or build step. Its three core files are:

- `site/index.html` defines the page sections and accessible controls.
- `site/styles.css` provides the responsive layout, colors, 3D-inspired artwork, and transitions.
- `site/app.js` powers progress tracking, project search and filters, clocks, the countdown, and rotating scenes and quotations.

The browser loads the CSS and JavaScript directly from the HTML. Keeping the first version dependency-free makes it easier to read, change, and deploy.

### 2. Build the page structure

In `site/index.html`, semantic sections organize the site: the navigation and hero, course countdown, roadmap, project ladder, learning approach, self-checks, resources, computing-history quotes, and footer. Headings label the sections, and the interactive elements have accessible names.

The page includes:

- A learning path with milestone checkboxes.
- Twelve progressively harder project cards with search and category filters.
- Free learning resources and short self-checks.
- A countdown toward an 18-calendar-month goal.
- An animated coding character and a separate rotating quotes panel.

### 3. Style it for desktop and mobile

`site/styles.css` contains the design system and layout. CSS Grid and Flexbox arrange the content; media queries adjust the navigation, hero, cards, and footer for smaller screens. Gradients, layered shadows, transforms, and keyframes create the orbital character and animated transitions without a 3D engine.

The layout also respects reduced-motion preferences. The character is an actual button, so it works with keyboard as well as pointer input.

### 4. Add browser interactions

`site/app.js` adds behavior without a framework:

1. It reads and saves checked roadmap milestones and projects in `localStorage`.
2. It filters projects by category and search text.
3. It computes the visitor's 18-month calendar deadline and updates the countdown each second.
4. It updates the visitor's local clock every second.
5. It rotates through five coding scenes every five seconds. Clicking the character immediately advances to the next scene.
6. It rotates sourced computing-history quotations every five seconds. The quote panel can be paused and resumed.

Progress and the countdown deadline are stored **only in the current visitor's browser**. They are not accounts, shared data, or a server-side visitor counter; clearing browser storage resets them.

### 5. Run it locally

No dependencies need to be installed. With Python 3 available, open a terminal at the repository root and run:

```powershell
py -m http.server 8000 --directory site
```

Then visit [http://localhost:8000](http://localhost:8000). You can also open `site/index.html` directly, but using a local web server more closely matches how the deployed site loads.

### 6. Publish changes and keep the site live

The workflow at `.github/workflows/deploy-pages.yml` publishes the contents of `site/` to GitHub Pages whenever changes to the site, README, or workflow reach `main`. It can also be started manually from the repository's **Actions** tab.

To publish an update:

1. Edit the files in `site/`.
2. Preview the site locally and check both desktop and mobile widths.
3. Commit the changes and push a branch.
4. Open a pull request into `main` and merge it after review.
5. Open **Actions** and confirm that **Deploy website** succeeds.
6. Visit the live link at the top of this README. The first Pages deployment may take a few minutes.

For a new GitHub Pages setup, open **Settings → Pages** and select **GitHub Actions** as the build and deployment source. The workflow uses the official Pages upload and deploy actions; no server needs to stay running on your computer. GitHub hosts the built static files continuously, while browser-side animations and timers run when a visitor opens the page.

## Project files

```text
.
├── .github/
│   └── workflows/
│       └── deploy-pages.yml   # Deploys site/ to GitHub Pages
├── site/
│   ├── app.js                 # Browser interactions and live timers
│   ├── favicon.svg            # Animated coding favicon
│   ├── index.html             # Page structure and content
│   ├── logo.svg               # Coding laptop logo and avatar animation
│   └── styles.css             # Responsive design and animations
└── README.md                  # This build and deployment guide
```

## Pull request history: how the website evolved

These are the 15 merged pull requests that built the original website in [Anujbarwal/Anujbarwal](https://github.com/Anujbarwal/Anujbarwal). They are linked to their original pull requests so you can inspect the actual diffs and review discussions. Their changes are already included in this standalone copy.

### Foundation and identity

1. [PR #1 — Add an interactive 3D full-stack roadmap website](https://github.com/Anujbarwal/Anujbarwal/pull/1)

   Established the complete static-site foundation: responsive layout, roadmap phases, project ladder, self-checks, resources, and browser-local progress tracking. It introduced the animated coding character and configured the first GitHub Pages deployment workflow. This created the site structure that later changes extended.

2. [PR #2 — Add animated coding favicon](https://github.com/Anujbarwal/Anujbarwal/pull/2)

   Replaced the basic tab icon with an animated SVG showing a developer at a laptop. The SVG uses vector shapes, gradients, and CSS animation, so it remains sharp at small favicon sizes without an image dependency.

3. [PR #3 — Add coding laptop site logo](https://github.com/Anujbarwal/Anujbarwal/pull/3)

   Added a reusable coding-laptop SVG brand mark and placed it in the site header and footer. Responsive sizing kept the icon balanced beside the wordmark.

4. [PR #4 — Cycle coding characters in site logo](https://github.com/Anujbarwal/Anujbarwal/pull/4)

   Added three distinct coder portraits to the SVG logo and animated them in a repeating 15-second cycle. The animation is self-contained in the SVG and does not need JavaScript.

5. [PR #5 — Add live local clock to roadmap](https://github.com/Anujbarwal/Anujbarwal/pull/5)

   Added the visitor's local time, seconds, and timezone in the footer. JavaScript updates a semantic `<time>` element once per second; it does not announce every tick to screen readers.

### Course countdown iterations

6. [PR #6 — Add 3D 18-month course countdown](https://github.com/Anujbarwal/Anujbarwal/pull/6)

   Introduced a personal 18-calendar-month course deadline, starting on a visitor's first visit and saved in that browser. The first presentation used a 3D analog clock with a live days/hours/minutes/seconds countdown. It also accounted for unavailable browser storage and reduced-motion preferences.

7. [PR #7 — Show live course countdown as code on digital watch](https://github.com/Anujbarwal/Anujbarwal/pull/7)

   Changed the clock face into a digital watch and presented the live time values in a syntax-highlighted code style. The saved deadline and per-second countdown logic were retained.

8. [PR #8 — Remove watch from live course countdown](https://github.com/Anujbarwal/Anujbarwal/pull/8)

   Removed the watch illustration while keeping the code-styled countdown in a responsive panel. The timer continued using each visitor's existing saved deadline.

9. [PR #9 — Replace course code block with live text timer](https://github.com/Anujbarwal/Anujbarwal/pull/9)

   Replaced the code panel with a simpler text display of the remaining days, hours, minutes, and seconds. This changed the presentation, not the underlying deadline behavior.

10. [PR #10 — Restore course countdown from PR 8](https://github.com/Anujbarwal/Anujbarwal/pull/10)

    Reverted PR #9's text-only presentation and restored PR #8's code-panel design. The countdown remained live and continued using the saved 18-month deadline. PR #9 remains in the original repository's history.

### Changing and interactive hero

11. [PR #11 — Add rotating coding quotes to hero animation](https://github.com/Anujbarwal/Anujbarwal/pull/11)

    Added five original coding encouragements to the animated hero. The quote, coder character, and orbital colors changed together every five seconds.

12. [PR #12 — Rotate all hero copy every second](https://github.com/Anujbarwal/Anujbarwal/pull/12)

    Expanded the rotating scene to include the hero kicker, headline, and description as well as its character and quote. The initial copy was preserved as the first scene.

13. [PR #13 — Slow hero rotation to five seconds](https://github.com/Anujbarwal/Anujbarwal/pull/13)

    Slowed the complete hero scene from one second to five seconds and softened the fade-and-lift transitions. Versioned asset URLs were added to help browsers load updated CSS and JavaScript after deployment.

14. [PR #14 — Make hero coding scene clickable](https://github.com/Anujbarwal/Anujbarwal/pull/14)

    Made the coding character a keyboard-accessible button. Clicking it immediately advances the headline, description, quote, character, and colors, while the five-second automatic rotation continues.

### Computing history quotes

15. [PR #15 — Add rotating computer science quotes section](https://github.com/Anujbarwal/Anujbarwal/pull/15)

    Added a separate quote card for public-domain computing-history passages from Charles Babbage and Ada Lovelace. It shows the author, book/source, and a link to the original text; it changes every five seconds with an animation and includes pause/resume controls.

### Connected profile and repository commits

- [Profile README integration — PR #16](https://github.com/Anujbarwal/Anujbarwal/pull/16) links the live site, this public source repository, this build guide, both repositories' commit histories, and every feature PR from the profile README.
- [Merged profile commit `743513b`](https://github.com/Anujbarwal/Anujbarwal/commit/743513b0186b77d547340db21874313bab25a99b) contains that README update.
- [Standalone publication commit `2dc7396`](https://github.com/Anujbarwal/Full-Stack-From-Zero-Roadmap/commit/2dc73969c4c79ad4604f347390254c708bbbe78b) initially published this website, deployment workflow, license, and build guide.

## Technology and scope

- HTML, CSS, and plain JavaScript; no framework or package dependencies.
- GitHub Pages hosting with GitHub Actions deployment.
- `localStorage` for personal progress and the course deadline.
- Public-domain passages linked to their Wikisource texts.
- No server-side accounts, database, or shared progress synchronization.

## License

The code in this repository is provided under the MIT License. See [`LICENSE`](LICENSE). Quotations are brief public-domain excerpts and link to the source texts.
