# João de Queiroz · Portfolio

An 8-bit, terminal-style portfolio for **João de Queiroz**, Senior Software Engineer (backend, .NET, AWS) in Rio de Janeiro, Brazil.

The page looks like a retro terminal session. It types out a welcome, then runs the `about` and `experience` commands by itself, so visitors see his work history without doing anything. After that they can explore with commands or buttons.

It's a static site built around one page, `index.html`. There's no framework, no build step and no dependencies apart from two Google Fonts.

## What's on the page

- **Welcome:** a typed greeting with his name, role and links to LinkedIn, email and GitHub, visible from the start.
- **About:** a short summary and three headline numbers: 7+ years, 300K+ vehicles on the Movida platform, 100+ integrations rewritten.
- **Experience:** a timeline of five roles, most recent first. Each has what the product does, three key results and the tech used. Clicking a company opens the full details.
- **Skills:** backend, data, architecture, cloud, integration, testing, languages, education and certificates.
- **Projects:** a few side projects, each with a link to its repo, plus a link to all his repos on GitHub.

## Commands

| Command | Shows |
| --- | --- |
| `experience` | Work history timeline |
| `about` | Summary and headline numbers |
| `skills` | Tech stack, languages, education, certificates |
| `projects` | Side projects from GitHub |
| `contact` | Email, LinkedIn, GitHub |
| `open <company>` | Full details for one role, e.g. `open movida` |
| `help` | List of commands |
| `clear` | Clears the screen |

Every command except `open`, `help` and `clear` also has a button under the prompt.

## Run it locally

Open `index.html` in a browser. To serve it locally instead:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy

The site is live at **https://joaogqueiroz.github.io** on GitHub Pages, deployed from the root of `main`. Every push to `main` publishes it in about a minute.

## Editing the content

All content is in the `<script>` block of `index.html`:

| What | Where |
| --- | --- |
| Contact links | `GH`, `LI`, `EMAIL` constants |
| Jobs | `jobs` array: `company`, `role`, `when`, `lead`, `key` (bullets shown in the timeline), `more` (extra bullets shown on `open`), `tags` |
| Side projects | `projects` array |
| About, skills and contact text | `commands` object |
| Intro sequence and typing speed | `intro()` function |

The job with `now: true` gets the **NOW** badge.

**Keep three copies in sync.** The same content also lives in:

- **`<main id="profile">`** in `index.html`: a static HTML copy for crawlers, AI agents and visitors without JavaScript. It's hidden when JavaScript runs.
- **`llms.txt`:** a Markdown summary for LLMs.
- **The JSON-LD block** in `<head>`: title, employer and skills as schema.org `Person` data.

When you change a job, skill or project, update all of them.

## Readable by search engines and AI

The terminal is built with JavaScript, and most AI crawlers don't run JavaScript. So the page also ships its content as plain HTML:

- **Static profile:** the full content in semantic HTML, shown only when JavaScript is off.
- **JSON-LD:** a schema.org `Person` with role, location, employer, languages, skills and `sameAs` links to LinkedIn and GitHub.
- **`llms.txt`:** a Markdown profile at `/llms.txt`, also linked from `<head>`.
- **`robots.txt` and `sitemap.xml`:** allow all crawlers and point them to the page.
- **Canonical URL and Open Graph tags:** for link previews on LinkedIn and chat apps, with a 1200×627 preview image (`og-image.png`).

## Design

- **Palette:** near-black `#03050b`, blue `#3b82ff`, cyan `#6fd3ff`, pale-blue text `#dce8ff`. All text meets WCAG AA contrast (4.5:1).
- **Type:** [Press Start 2P](https://fonts.google.com/specimen/Press+Start+2P) for headings, buttons and numbers. [VT323](https://fonts.google.com/specimen/VT323) at a large size for everything people need to read.
- **Favicon:** a 16×16 pixel bug in the UI blue on black (`favicon.svg`).
- **Details:** a pixel window with a hard drop shadow, faint scanlines, a blinking block cursor, and buttons that press down.

## Accessibility

- **Skipping the intro:** click anywhere, press any key or use **SKIP INTRO**. The contact links are visible from the start, so nothing important waits for the animation.
- **Reduced motion:** visitors whose device is set to reduce motion see everything straight away, without typing.
- **Other support:** new output is announced to screen readers, and every button and link has a visible keyboard focus state.
- **Mobile:** the layout adapts to phone screens.

## Content sources

- **Experience:** João's LinkedIn profile.
- **Side projects:** his public GitHub, [@joaogqueiroz](https://github.com/joaogqueiroz).
