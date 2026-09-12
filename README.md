# Deploy and Host a Linux Desktop (Ubuntu XFCE) on Railway

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/new/template/linux-desktop?utm_medium=integration&utm_source=button&utm_campaign=linux-desktop)

This template runs a full Ubuntu desktop with the XFCE environment in the cloud, streamed to any device through the [linuxserver.io Webtop](https://docs.linuxserver.io/images/docker-webtop/) Selkies web interface. Open your Railway domain, log in, and you have a real Linux desktop with a terminal, file manager, browser and `sudo`. Installed packages, files and settings under the home directory persist between visits.

## About Hosting a Linux Desktop

The service streams a GPU-less XFCE desktop over WebSockets with the linuxserver.io Selkies stack. Access is gated by HTTP basic auth (`CUSTOM_USER` / generated `PASSWORD`), and the user's home persists on a volume at `/config`. Set `TITLE` to change the browser tab name.

## Common Use Cases

- A persistent Linux workstation reachable from an iPad, Chromebook, phone or locked-down work laptop
- Run GUI apps in the cloud: a browser with extensions, an editor, a chat client, an IDE
- Disposable sandbox for opening untrusted files or links away from your real machine
- Shared desktop for a team: one URL, one login, same session state

## Dependencies for Linux Desktop Hosting

- None. Single service, no database.

### Deployment Dependencies

- [linuxserver.io Webtop image docs](https://docs.linuxserver.io/images/docker-webtop/)
- [Selkies project](https://github.com/selkies-project)

### Implementation Details

**First use:** open your Railway domain, log in with `CUSTOM_USER` and the generated `PASSWORD` (service Variables tab), and the desktop appears. On touch devices, use the sidebar for keyboard and gestures. The desktop user `abc` has passwordless `sudo`, so `sudo apt install` works from the built-in terminal.

Notes and limits:

- Keep the login strong: the password gate is the whole security model for a desktop with sudo.
- Only `/config` (the home directory) persists. Packages installed with `apt` live outside it and are gone after a redeploy; reinstall them or keep a setup script in your home.
- Rendering is CPU-based (no GPU on Railway). Fine for desktop apps and light video; not for 3D or heavy media work.
- Idle footprint is about 250 MB, so it boots fine on the 512 MB Trial plan. Give it 1-2 GB if you run a browser or an IDE inside.
- The virtual screen is capped at 4K (`MAX_RES=3840x2160`); the desktop still resizes to your browser window. Raising the cap costs RAM: the upstream default of 15360x8640 needs ~600 MB for the framebuffer alone.
- No Docker daemon inside the desktop.
- Looking for just a browser? The same author publishes [Chromium](https://railway.com/deploy/chromium), [Google Chrome](https://railway.com/deploy/google-chrome), [Firefox](https://railway.com/deploy/firefox-browser), [Brave](https://railway.com/deploy/brave-browser) and [Microsoft Edge](https://railway.com/deploy/microsoft-edge) templates.

## Why Deploy a Linux Desktop on Railway?

Railway is a singular platform to deploy your infrastructure stack. Railway will host your infrastructure so you don't have to deal with configuration, while allowing you to vertically and horizontally scale it.

By deploying a Linux desktop on Railway, you are one step closer to supporting a complete full-stack application with minimal burden. Host your servers, databases, AI agents, and more on Railway.
