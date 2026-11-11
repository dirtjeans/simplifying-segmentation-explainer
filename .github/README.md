# Simplifying Segmentation: seven simple steps

An interactive, animated explainer for the Illumio e-book
*Simplifying Segmentation: The Missing Layer in a Broken Security Model*.

It walks through a seven-step microsegmentation rollout on an animated map of
a generic enterprise. It ends with a call to action that links to the e-book:
<https://www.illumio.com/resource-center/simplifying-segmentation>

## What is in this repo

| Path | What it is |
| --- | --- |
| `index.html` | The whole explainer: markup, styles, script, and the soundtrack |
| `img/` | The e-book cover shown on the ending screen |
| `webflow.json` | Tells Webflow Cloud this is a static app (not published) |
| `.github/README.md` | This file (not published) |

There is no build step and no framework. The soundtrack and sound effects are
generated in the browser with the Web Audio API, so there are no audio files.

## Fonts

The page uses FK Grotesk only. It is licensed to Illumio.

The font files are **not** in this repo. The page loads them from the custom
fonts stored on the Illumio Webflow site, the same files illumio.com uses:

| Weight | File on the Illumio Webflow site |
| --- | --- |
| Light 300 | `6707c08c58e8fda5d4ff68dd_FKGrotesk-Light.woff` |
| Regular 400 | `6707c08ccf04d235d6f3fe38_FKGrotesk-Regular.woff` |
| Medium 500 | `6707c08c2e531c0b456b1304_FKGrotesk-Medium.woff` |
| Bold 700 | `6707c08d3ce6f76b01ec3b00_FKGrotesk-Bold.woff` |

If the web team replaces those font files in Webflow, update the four
`@font-face` addresses and the four `preload` links at the top of `index.html`.

## Deploying on Webflow Cloud

This is a no-framework static app. Webflow Cloud serves the files exactly as
committed, at the mount path set for the environment.

- Keep `index.html` at the repo root, and do not add a `package.json`.
- Every public file in the repo is published. Files and folders that start
  with a dot, and `webflow.json`, are not.
- Paths inside the page are relative, so the mount path can change without
  code edits. The page works with or without a trailing slash.
- Pushing to the connected branch deploys a new version.

## Run it locally

Serve the folder with any static web server, then open the address it prints.

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Controls

| Control | What it does |
| --- | --- |
| Space | Play or pause (pausing also pauses the music) |
| Left and right arrows | Previous or next screen |
| 1 to 7 | Jump to a step |
| M | Mute or unmute all sound |
| Bottom bar | Back, play or pause, next, step links, sound, full screen |

Viewers can also choose "Go at my own pace" on the title screen. The explainer
then waits on each screen until they press an arrow.

## Common edits

All of these live in `index.html`.

| To change | Search for |
| --- | --- |
| The e-book link | `GUIDE =` |
| The ending headline and text | `Put the seven steps to work` |
| Step names and screen copy | `const PH =` |
| Music level (sound effects are separate) | `MUSIC =` |
| Overall volume | `VOL =` |
| Title screen copy | `Seven simple steps` |
| Browser tab title and description | `<title>` |

## Notes

- Some on-screen figures are illustrative, not real data. These include the
  allowed-paths count, the port numbers, and the time-lapse day counter.
- The page follows the Illumio Design System: Illumio Orange, the dark cyan
  surfaces, sentence case, and no ligatures.
- Most movement is toned down for viewers whose system asks for less motion.
