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
| `.github/embed-snippet.html` | Optional snippet for a host page with a navigation bar (not published) |
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

## Where it lives on illumio.com

| Address | What it is |
| --- | --- |
| `/interactive-tools/simplifying-segmentation-explainer` | The public page. It is an item in the Interactive Tools CMS collection, like the other interactive tools, so it gets the same page template and footer. Its "Show Site Navigation" switch is on, so it also gets the site navigation bar. |
| `/apps/simplifying-segmentation-explainer` | This repo, served by Webflow Cloud. The CMS item's "Iframe Embed Link" field points here. |

To list the explainer on `/resources/interactive-tools`, give the CMS item a
Sort Order, a headline, an intro paragraph, a preview image, and button text.
With a blank Sort Order it stays off that list.

The "Show Site Navigation" switch on a CMS item shows the Global / Navbar
component above that tool. It is off for the other tools, which fill the
whole screen. In the page template the navigation bar sits in a wrapper block
(class `interactive-tool_nav-wrap`) whose visibility follows the switch.

## Deploying on Webflow Cloud

This is a no-framework static app. Webflow Cloud serves the files exactly as
committed, at the mount path set for the environment
(`/apps/simplifying-segmentation-explainer`).

- Keep `index.html` at the repo root, and do not add a `package.json`.
- Every public file in the repo is published. Files and folders that start
  with a dot, and `webflow.json`, are not.
- Paths inside the page are relative, so the mount path can change without
  code edits. Webflow Cloud adds a `<base>` tag for the mount path, and the
  page relies on it there.
- Pushing to the connected branch deploys a new version.
- The Illumio site adds its usual analytics and marketing tags to the page
  on its own. None of them are in this repo.
- Do not mount the app under `/interactive-tools/`. That path belongs to the
  CMS collection, and an app mounted there hides the collection page.

## How it behaves inside a frame

The explainer is on the same site as the pages that frame it, so it can look
after itself:

- **No second scroll bar.** On phones and narrow or tall frames the explainer
  stacks its layout and makes its own frame as tall as the content, so only
  the page scrolls. On wide frames it keeps the height the page gives it and
  scales to fit.
- **It fits under the site navigation.** If the host page has a bar stuck to
  the top, the explainer shortens its frame to the space below the bar and
  hides its own logo, since the bar already shows one.
- **Campaign tags carry over.** Any `utm_` tags on the host page's address are
  added to the e-book link. The same happens when the explainer is opened on
  its own with `utm_` tags.
- **Full screen** works in frames on the same site. If a frame may not go full
  screen, the button hides itself.
- Space and the arrow keys work only after a click inside the frame.
- The site adds its analytics tags to the explainer as well as the host page,
  so a framed visit can count twice. Exclude `/apps/` in the tag setup if that
  matters.

### On a page outside the Interactive Tools template

`.github/embed-snippet.html` is for a host page built by hand, with the site
navigation above the frame. Its frame address ends in `?embed=1`, which hides
the explainer's own logo and lets the snippet size the frame to fit under the
bar. Paste it into one Code Embed element. The Interactive Tools page does not
need it.

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
