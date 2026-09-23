# BYS AI funnel — clickable prototypes

BuildYourStore's step-based store builder, reimagined as a scripted conversation.
Everything here is static HTML: no build step, no dependencies, no data leaves the page.

**Open [`index.html`](index.html)** — it lists every page with a line on what each one is for.

## The one to look at

[`bys-funnel.html`](bys-funnel.html) runs the whole funnel, nine steps end to end, and
switches between the desktop and the mobile layout **with the width of the window**. Drag
the edge of the browser, or use the device toolbar in dev tools — the breakpoint is 768px.

What changes when it goes narrow is not only the layout:

- answers, buttons and CTAs move to the right edge, so everything the user presses is on one side
- the progress ring leaves the bottom-right corner and takes the left, which the controls have vacated
- replies arrive one at a time rather than as a block — a turn waits out the time it takes to read the turn before it
- a focused field lifts clear of the band the keyboard will occupy
- modals come off the bottom edge as sheets
- the six prototype switches fold behind the **Prototype** button in the nav

There is no phone frame and no fake status bar. At narrow widths this is the interface
itself, the way dev tools shows it.

## The switches

In the nav on a wide window, behind **Prototype** on a narrow one. They exist so the failure
states can be reached without playing the funnel until one happens by chance:

| Switch | What it does |
|---|---|
| States | Shows the three assistant waiting states side by side |
| Publish: works / fails | The Shopify publish check keeps failing until you switch it back |
| Build: works / fails | The store build fails; **Try again** keeps failing until you switch it back |
| Offer: 10 min / 10 sec | Runs the downsell countdown at 10 seconds, so the expired state can be reviewed |
| Domain: free / taken | The first suggested domain turns out to be taken |
| Restart | Reloads from the first question |

## The other pages

`bys-funnel-v2.html` and `bys-funnel-mobile.html` are the two single-width files the
responsive one was merged from, kept so there is something to compare against. The mobile
one draws a phone with a status bar — that frame is the mockup, and is deliberately absent
from the responsive file.

The rest hold one moment still so it can be looked at without playing through to reach it:
coming back after a break, a finished step opened in place, the domain failure states, the
downsell card on its own.

## Notes for anyone reading the code

- One file per prototype. The stylesheet mirrors the Figma token names 1:1; nothing uses a raw literal.
- The mobile layer is a single `@media (max-width: 768px)` block at the end of the stylesheet, and the script asks the same media query, so the two cannot disagree about which layout is on screen.
- `prefers-reduced-motion` is honoured throughout.
- The payment sheet's card fields are `readonly`. This is a design prototype and it collects nothing.
