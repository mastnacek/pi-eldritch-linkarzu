# pi-eldritch-linkarzu

An [omp](https://github.com/can1357/oh-my-pi) colour theme built from the Linkarzu
kitty theme — his own take on Eldritch, with the signature pink `#f94dff` cursor
carried over as the accent.

All 67 required colour tokens are set from that palette.

## Install

```sh
git clone https://github.com/mastnacek/pi-eldritch-linkarzu.git
cp pi-eldritch-linkarzu/eldritch-linkarzu.json ~/.omp/agent/themes/
```

Then select it. Either through the TUI:

```
/settings  →  Appearance  →  Dark Theme
```

or from the CLI:

```sh
omp config set theme.dark eldritch-linkarzu
omp config set theme.light eldritch-linkarzu
```

The theme file is watched while omp runs — save a change and it reloads in place
without a restart.

## Two settings worth turning on

Neither is a theme-file concern, but the theme will not fully apply without them.
Copy from `omp-config-snippet.yml` or set directly:

```sh
omp config set statusLine.sessionAccent false
omp config set display.shimmer classic
```

**`statusLine.sessionAccent: false`** — the default `true` derives the
session-name colour from a djb2 hash of the session name, clamped to hue 0–120°
(red → yellow → green). The signature pink can never appear in that band, so the
status line never showed it. With `false`, the segment uses `statusLineModel`,
which points at the pink.

**`display.shimmer: classic`** — the loading shimmer has three styles. `kitt` is a
Knight Rider scanner bouncing left-right at 30 cells/s; `classic` is a soft cosine
sweep. Unrelated to colour, but it is the fastest-moving thing in the TUI.

## Things that look like they should be themeable but are not

Both of these cost real time to track down, so they are written down here.

**Empty `text` / `userMessageText` do not mean "terminal default".** The theme
schema documents `""` as terminal default, and for most tokens that is what
happens. But `text` goes through `fgResolved()` and `userMessageText` goes through
`fgOnBg()`, and both replace an empty value with a hardcoded `#e5e5e7` — a grey
that is not in this palette. Both are set to `star` (`#ebfafa`) in the shipped
theme. Do not "tidy" them back to `""`.

`customMessageText` is left as `""` on purpose: it goes through plain `fg()`, where
empty really does mean terminal default.

**Spinner and blink rates are not configurable.** There is no `animationSpeed`,
`fps` or `cadence` setting in `settings-schema.ts`. The cadences are compile-time
constants:

| Animation | Rate | File |
|---|---|---|
| Loader shimmer redraw | 30 fps (`1000/30`) | `packages/tui/src/components/loader.ts` |
| Loader spinner advance | 80 ms | `packages/tui/src/components/loader.ts` |
| Tool execution spinner | 80 ms render + 80 ms glyph | `modes/components/tool-execution.ts` |
| Status line speculation blink | 600 ms | `modes/components/status-line/component.ts` |
| Welcome intro | 3000 ms, tick 33 ms | `modes/components/welcome.ts` |

Slowing these means patching the constants and rebuilding. The shimmer is the only
one exposed as a setting.

## Verifying a change

```sh
omp gallery --width 100              # every tool renderer
omp gallery --surface composer       # all 8 composer shapes
omp gallery --surface segment        # status line segments
```

`omp gallery --screenshot` writes a real PNG but needs `vhs` installed; without it
only ANSI reaches stdout.

Two tokens never appear in a normal gallery or session and need a deliberate probe
to exercise: `selectedBg` (only painted on a mouse-hover row in a select list) and
`customMessageBg` (only on hook, skill and compaction messages).

## Layout

| File | |
|---|---|
| `eldritch-linkarzu.json` | the theme — all 67 tokens plus an `export` block for HTML session export |
| `palette-source.md` | which kitty colour became which token, and the WCAG numbers behind the two derived greys |
| `omp-config-snippet.yml` | the three settings, with the reasoning |

## Credit

Palette from [Linkarzu's dotfiles](https://github.com/linkarzu), whose kitty config
is described as *"Linkarzu vlastní (Eldritch-inspired)"*. Base idea from
[eldritch-theme/kitty](https://github.com/eldritch-theme/kitty) by jacobreeda, MIT.
