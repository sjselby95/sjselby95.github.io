# sjselby95.github.io

Personal portfolio site for Steven Selby — documenting a career transition from commercial truck driving into IT and cybersecurity.

## Live site

https://sjselby95.github.io

## Current state

The site has been rebuilt as an interactive SVG motherboard layout. Each section of the page is represented as a physical component on the board (CPU, RAM, M.2 slots, chipset, etc.), with a responsive mobile fallback nav for smaller screens.

## Pages

- **index.html** — Main landing page (motherboard layout)
- **about.html** — About section, themed as a CPU / silicon die
- **certifications.html** — Certifications displayed as a DDR5 RAM stick with DRAM chip cards
- **software.html** — Software list, themed as a BIOS setup utility
- **projects.html** — Projects, themed as an M.2 NVMe SSD with a directory listing
- **labs.html** — Labs, themed as a hypervisor / VM console
- Photography and Contact are not standalone pages — those links point to the Flickr profile and a `mailto:` respectively
- `terminal.html` — CMOS-battery easter egg, not yet built

## What was done in this session

- Extracted all inline CSS from `index.html` into `styles.css`
- Added **Russo One** font (Google Fonts) for the name plate — more visual impact
- Added a custom **SVG favicon** (motherboard/PCB design, green on black)
- Added **headshot** (`headshot.jpg`) clipped into a circle on the CPU/About component
- Added headshot to the **mobile nav** as a circular avatar above the name
- **Contact component**: moved label above the box, added email address inside, wired to `mailto:sjselby95@gmail.com`
- **RAM/Certifications**: moved "Certifications" label above the sticks, made slots 1 & 3 full RGB with a seamless top-to-bottom flowing animation, tightened the bounding box to fit 4 sticks
- Built **certifications.html** — RAM stick layout with browser chrome mockup, RGB diffuser strip, 8 DRAM chip cards (2 earned, 6 open slots), gold contact fingers footer, and nav bar
- A+ and IBM IT Support Professional chips link to their respective **Credly badges**
- Removed `.claude/launch.json` files from both projects to stop auto-launching the preview panel on file edits

## Built with

- HTML
- CSS
- SVG (layout, animation)
- Google Fonts: JetBrains Mono, Russo One
