<div align="center">

# 🍅 flowstate

### A tty-clock-style Pomodoro countdown for Hyprland + kitty

Big block digits centered **inside a terminal**, session progress on a line
below — **4 × (25 min focus + 5 min break)**, every timer always counting
down. Focus is muted grey, break is red. No Spotify, no music, no
dependencies beyond kitty + hyprctl — a single bash script.

</div>

> Inspired by [tty-clock](https://github.com/xorg62/tty-clock) and the
> [omarchy-flowstate](https://github.com/keegan-sucks/omarchy-flowstate)
> bar widget, rebuilt for a custom quickshell rice.

---

## What it does

- Opens a normal **tiling kitty** (or any terminal: run `flowstate.sh run`
  inside one) and draws a big 7-segment countdown in the middle of it
- Progress line below the clock: `⌖ focus 2/4 · ●●○○`
- Phase bells at each boundary (freedesktop sounds via `pw-play`), a desktop
  notification when the session completes
- A quickshell bar chip reads `~/.local/state/flowstate/bar` and shows the
  live countdown, colored to match the current phase

## Install

Works on any Hyprland setup; this repo was built for a quickshell + hyprland
Lua config. Drop the script anywhere on your `$PATH` or in `~/.config/hypr/`:

```sh
cp flowstate.sh ~/.config/hypr/ && chmod +x ~/.config/hypr/flowstate.sh
```

Optional keybind (Hyprland Lua config):

```lua
hl.bind("SUPER + SHIFT + L", hl.dsp.exec_cmd("kitty -e bash ~/.config/hypr/flowstate.sh run"))
```

The bar widget (in your `Bar.qml`) shows a `⌖` chip that toggles the session,
middle-click pauses, right-click stops.

## Usage

```sh
./flowstate.sh          # toggle: launch a timer kitty, or close one
./flowstate.sh run      # render the clock in the current terminal
./flowstate.sh pause    # pause/resume the running session (SIGUSR1)
./flowstate.sh stop     # end the session
```

Inside the timer window: **space** = pause/resume · **q** = quit.

## Tunables (environment)

| Var | Default | Meaning |
|---|---|---|
| `FOCUS_MIN` | 25 | Focus minutes |
| `BREAK_MIN` | 5 | Break minutes |
| `CYCLES` | 4 | Focus + break pairs per session |
| `SCALE` | 2 | Digit size (1 or 2) |
| `FONT_SIZE` | 16 | kitty font size at launch |
| `SOUND` | 1 | Phase bells (`0` to disable) |
| `NOTIFY` | 1 | End notification (`0` to disable) |

## License

MIT — see [LICENSE](LICENSE).
