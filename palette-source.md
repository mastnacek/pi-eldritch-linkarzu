# Source palette

Extracted from the Linkarzu kitty theme (`~/.config/kitty/linkarzu.conf`), which is
itself described upstream as *"Linkarzu vlastní (Eldritch-inspired), RŮŽOVÝ kurzor
#f94dff"* — Linkarzu's own take on the Eldritch theme, not the upstream jacobreeda
version.

| Role | Hex | Where it landed in the omp theme |
|---|---|---|
| background / black | `#0D1116` | terminal default (kept as `""` so kitty opacity/blur still shows) |
| foreground / white | `#ebfafa` | `star` → `text`, `userMessageText`, `mdCode`, `syntaxVariable` |
| **cursor (signature)** | `#f94dff` | `pink` → `accent`, `borderAccent`, `mdHeading`, `syntaxKeyword`, `thinkingMax`, `statusLineModel` |
| selection | `#e9b3fd` | (unused — terminal owns selection colour) |
| red | `#f16c75` | `error`, `toolDiffRemoved`, `statusLineUntracked` |
| green | `#37f499` | `success`, `toolDiffAdded`, `statusLineGitClean` |
| yellow slot | `#19dfcf` | `warning` — Linkarzu deliberately remapped yellow to teal |
| blue | `#987afb` | `syntaxType`, `thinkingXhigh`, `statusLineSpend`, `pythonMode` |
| magenta | `#949ae5` | `border`, `thinkingHigh`, `statusLineSubagents` |
| cyan | `#04d1f9` | `mdLink`, `syntaxFunction`, `statusLinePath` |
| bright black | `#5fa9f4` | (not used — omp has no bright-black token) |

Linkarzu's palette has no grey ramp, so the two neutral tokens are derived to keep
WCAG contrast readable on the `#0D1116` surface:

- `muted` `#838ca2` — 5.09:1 on the tool panel
- `dim` `#616b80` — 3.20:1 on the tool panel

An earlier `#4d5566` for `dim` measured 2.29:1 and was too low for the syntax
comments that use it.

Surface shades are interpolated off the background:

| Token | Hex |
|---|---|
| `panel` → `userMessageBg`, `toolPendingBg` | `#161C24` |
| `panelAlt` → `customMessageBg` | `#1B222C` |
| `surface` → `selectedBg` | `#242C38` |
| `borderCol` → `borderMuted`, `statusLineSep`, `mdHr` | `#2A323E` |
| `statusLineBg` | `#101419` |
| `toolSuccessBg` | `#0F1A18` |
| `toolErrorBg` | `#1F1418` |
