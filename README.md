# KAWS Theme for DeepSeek Harness

A personal Web UI theme built around the KAWS Companion vocabulary: charcoal
and bone, crimson and teal, XX eyes, chunky button edges, and a faint
streetwear watermark. It is a client-only DSH bundle; the host half is
intentionally empty.

## What it changes

- Both Light and Dark palettes, with every alias token supplied for both modes.
- Charcoal/bone hierarchy with crimson focus, selection, and send accents,
  plus teal secondary marks.
- A large Companion artwork watermark across the bottom-left of the conversation canvas,
  feathered into the background.
- A flat canvas: the window surface is one solid colour from the title bar down to
  the floor. There is no corner glow and no teal floor ramp, in the new-session
  state or in a conversation; the transparency rules only keep the columns and the
  composer band from cutting it with their own fills.
- A flat composer: the input card is one opaque teal plate with a hairline edge —
  no offset sticker shadow, no backdrop blur, and a plain crimson hairline on
  focus. The same plate is used in the hero and in a conversation.
- A Light/Dark switch in the top banner, beside the Session utilities, as a
  compact icon button with a tooltip (it no longer sits at the sidebar foot).
- A sidebar brand row that greets instead of branding: the product wordmark is
  replaced by `Good morning, Sean.` before noon, `Good afternoon, Sean.` until
  17:00, and `Good evening, Sean.` after that (and overnight). The Companion
  mark and the row's new-session/toggle behavior are unchanged.
- A crimson-to-teal radial wash on the sidebar: a crimson pool over the brand row
  and a teal pool above the settings foot, both centred on the rail and continued
  across the Windows titlebar strip above it, with Companion-head replacements for
  the small brand glyph and the hero mark.
- Offset sticker shadow on New Session; the composer, its focus state, and the
  send disc stay flat.
- Crimson scrollbars, translucent crimson text selection, focus rings, and matching Appearance cubes.

## Install

From the DSH Web GUI: **Plugins → Add plugin → local directory path**, then enter
this directory and choose **Install → Enable now**.

The bundle also works through `plugin_manager` with `action: install_bundle` and
this directory as the `target`.

## Files

| File | Role |
|---|---|
| `index.js` | Host half; empty plugin row that keeps the bundle active. |
| `client.js` | Client half; registers token overrides, the stylesheet, and the mode button. |
| `companion.png` | Companion line art, embedded as a bottom-left alpha-mask watermark. |
| `cordis.patch.yml` | Bundle patch that inserts the `kaws-theme` row. |
| `icon.svg` | Plugin Manager artwork. |
| `locale/*.json` | Plugin Manager title and description. |

## Notes

The theme is an override layer, not a new preference value. It composes on top
of the built-in Light/Dark/System choice, so the normal Appearance controls keep
working. The banner switch writes a normal Light or Dark preference when clicked;
it is registered in `conversation.session.header.utilities`, so it shows while a
Session is open. Removing or disabling the bundle restores the host palette and
removes the stylesheet.

The greeting is a slot occupant, not a DOM patch: `sidebar.brand.name` is a
single slot whose lowest-priority registration renders, so the row registers at
priority `-1` and shadows the official wordmark while `ui-brand-official` stays
installed. The mark slot is untouched. Change `GREETING_NAME` and the hour
boundaries in `greetingAt()` in `client.js` to retarget it; a reload picks the
change up.
