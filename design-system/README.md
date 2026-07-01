# נשמה · Design System

A new visual language for the Neshama app: **Jewish blue & white with delicate, light gold
accents**, replacing the legacy cream/peach + terracotta-orange theme. The calm, premium,
watercolor feel and rounded-card layout are retained.

## Files
- **`index.html`** — a self-contained, RTL/Hebrew visual showcase: color & type foundations
  and every component (buttons, option rows, day-circle journey, streak, cards, chat, reader
  with selection toolbar, tab bar, paywall, notifications). Open it in any browser.
- **`screens.html`** — full phone-frame mockups of every major screen in the new palette:
  splash, onboarding steps (gender, goals, age, name, nusach, reading level), personalized
  value + chart, streak, notification priming, paywall, Today, Tehillim, Siddur, Tanakh,
  Chat, and Settings.
- **`tokens.css`** — the shared design tokens (palette, gradients, elevation, radii, type) as
  CSS custom properties for implementation.

## Palette
| Role | Token | Hex |
|---|---|---|
| Primary navy | `--blue-800` | `#102A43` |
| Primary blue | `--blue-700` | `#1E3A5F` |
| Accent blue | `--blue-600` | `#2C5F8A` |
| Soft blue | `--blue-300` | `#9FC3E0` |
| Tint background | `--blue-050` | `#EEF5FB` |
| Surface | `--white` / `--paper` | `#FFFFFF` / `#F7FAFC` |
| Gold accent | `--gold-500` | `#C8A24B` |
| Soft gold | `--gold-400` | `#D8B968` |
| Faint gold wash | `--gold-200` | `#E9D6A0` |

> **Gold is intentional and minimal** — used only for thin dividers, small icon strokes,
> active states, and delicate corner flourishes. No heavy gold fills.

## Typography
- **UI:** Heebo / Assistant (clean Hebrew sans), RTL.
- **Verse & prayer:** Frank Ruhl Libre (refined Hebrew serif) with full nikud support.

## Using this with Claude Design (claude.ai/design)
This session runs in Claude Code on the web, where the Design-System cloud sync
(`DesignSync` / `/design-sync`) cannot authenticate interactively. To publish these into a
Claude Design project, either:
1. Open the project in **claude.ai/design** and use **"Send to Claude Code Web"** to seed it
   into the workspace, then re-run `/design-sync`; or
2. Upload `index.html` / the component HTML directly into a Design-System project.

Each component block in `index.html` is grouped under a labelled section so it maps cleanly to
Design-System preview cards.
