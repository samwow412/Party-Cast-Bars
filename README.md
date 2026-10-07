<img width="508" height="303" alt="image" src="https://github.com/user-attachments/assets/eb652618-6a77-4fb6-9699-56e4262b68ae" />

# Party Cast Bars

Clean, minimal cast bars for your party, attached to the right side of each raid-style party frame. Built for **World of Warcraft: Forever** and designed around Midnight-style secret values, so it keeps working in combat.

## Features

- **One cast bar per party member**, anchored to the matching raid-style party frame (yours included, optionally).
- **Casts and channels** with a spell icon, spell name, timer, and spark.
- **Not-interruptible indicator**: a grey overlay shows when a cast can't be interrupted.
- **Interrupted / Failed flash** with configurable hold and fade times.
- **Secret-value safe**: bar progress is driven by duration objects (`UnitCastingDuration` / `UnitChannelDuration` with `StatusBar:SetTimerDuration`). Spell names, icons and interruptible state go straight to display functions and are never read by Lua. If the client doesn't provide those APIs, the addon falls back to plain start/end times.
- **Live preview mode** with demo casts, channels, non-interruptible casts and interrupts. If no party frame is visible, the preview bars float near the screen center.

## Settings GUI (`/pcb`)

<img width="1288" height="1143" alt="image" src="https://github.com/user-attachments/assets/258a8548-2030-4dc6-99e3-154291b79f19" /> <img width="1264" height="1117" alt="image" src="https://github.com/user-attachments/assets/652689e4-a80b-4728-90e5-81a56a778fda" />

| Tab | Options |
|---|---|
| **General** | Enable, show my own bar, preview toggle, frame name pattern, frame count, reset |
| **Position & Size** | Right / Left / Below / Above presets, bar and frame anchor points, X/Y offsets, width, height (or match party frame height), scale, opacity, frame strata |
| **Bar** | Texture, reverse fill, channels drain, smooth animation, background, border (size/color), spark (width/color), spell icon and side |
| **Colors** | Cast, channel, not interruptible, interrupted/failed |
| **Text** | Font, outline, color, padding, spell name (size/alignment), timer (size, remaining or elapsed, decimals) |
| **Interrupts** | Flash on interrupt/fail, hold time, fade time |

Textures and fonts are picked up from [LibSharedMedia-3.0](https://www.curseforge.com/wow/addons/libsharedmedia-3-0) if any other addon provides it. Without it, a built-in Solid and Blizzard texture and the default font are used.

## Installation

1. Download the latest release.
2. Extract the `PartyCastBars` folder into your WoW Forever `Interface/AddOns` directory.
3. Run `/reload` or restart the game.

Ace3 libraries are bundled in `Libs/`; nothing else is required.

If the addon shows as out of date, run `/dump (select(4, GetBuildInfo()))` and put that number in the `## Interface:` line of `PartyCastBars.toc`, or tick "Load out of date AddOns".

## Slash commands

| Command | Action |
|---|---|
| `/pcb` | Open the settings |
| `/pcb test` | Toggle preview bars |
| `/pcb diag` | Show which party frames were found and which API path is in use |
| `/pcb reset` | Reset all settings |

## Using other frame addons

By default bars attach to frames named `CompactPartyFrameMember1` to `CompactPartyFrameMember5`. If you use different party frames, find their names with `/fstack`, then set **General > Frame name pattern** (use `%d` for the frame number, e.g. `MyPartyFrame%d`) and the number of frames. The frames need to expose their unit as a `unit` field or attribute.

## Known limitations

- Empowered casts are not handled (not applicable to Forever's Classic-based spell set).
- Cast timer text depends on the client accepting secret numbers in `FontString:SetFormattedText`. If it doesn't, the timer is disabled and the bar keeps working (`/pcb diag` reports this).
- Written against the documented 12.x API; please report any differences you see on Forever.

## Support / Issues

Please open an issue and include the output of `/pcb diag` and any Lua error text.

## Credits and license

- Uses [Ace3](https://github.com/WoWUIDev/Ace3) (AceGUI-3.0, AceConfig-3.0, CallbackHandler-1.0, LibStub), included under its license (`Libs/Ace3-LICENSE.txt`).
- Addon code is released under the [MIT License](LICENSE).
