# Lightbrowse Implementation Roadmap

## Goal

Build a lightweight custom browser for Windows with Python, PySide6, and Qt WebEngine. Start with a usable browser shell, then add voice control and safety boundaries in independently verifiable stages.

## Guiding decisions

- Do not fork a full browser distribution.
- Initial supported and verified platform: Windows.
- Use Python with official PySide6 bindings and Qt WebEngine.
- Build separate binaries on each operating system; do not promise one binary works across Windows, macOS, and Linux.
- Do not add a password manager or save login sessions.
- Select the project license after implementation dependencies and redistribution terms are known.
- Keep browser content untrusted. Voice commands may invoke only explicit browser actions; page text must never become executable instructions.

## Stages and completion criteria

### Stage 0 — Repository and build foundation

- Add a clear project README with the scope, supported platform, setup instructions, and current non-goals.
- Add a reproducible Python environment and dependency declarations for PySide6 / Qt WebEngine.
- Establish a minimal app entry point and a documented Windows development command.
- Record Qt, PySide6, Python, and WebEngine versions used during development.
- Defer final project-license selection; maintain an inventory of bundled dependency licenses and video-codec constraints.

**Complete when:** a clean Windows checkout can create the documented environment and launch the app entry point.

### Stage 1 — Open a minimal browser window

- Create a PySide6 desktop window containing one Qt WebEngine view.
- Load a default safe page and allow a URL to be entered.
- Show basic loading and failure state so the initial blank screen is diagnosable.
- Keep the layout minimal; no tabs, extensions, bookmarks, or voice recognition yet.

**Complete when:** the app opens as a desktop browser window, loads a page, and can navigate to another URL on Windows.

### Stage 2 — Basic browser navigation

- Add address entry, back, forward, reload, and stop controls.
- Synchronize the address bar with the current page and handle redirects.
- Add a small allowlist/guard for supported URL schemes; external/custom schemes do not launch arbitrary handlers.
- Verify YouTube search and playback behavior; document any codec or DRM limitations found.

**Complete when:** normal HTTP(S) browsing, YouTube search, playback, and basic navigation work in the Windows build.

### Stage 3 — Ephemeral session and action boundaries

- Create an explicit off-the-record Qt WebEngine profile for all browser pages.
- Keep cookies, cache, local storage, permissions, and browsing history in memory only.
- Disable password storage/autofill and do not provide a password manager.
- Add a navigation policy that blocks or warns on sign-in/authentication destinations, and test redirects and popups.
- Deny downloads and permission prompts by default until a safe explicit policy exists.
- Document that profile ephemerality reduces local persistence but is not a complete security sandbox.

**Complete when:** automated checks and manual inspection show the profile is off-the-record, and closing/reopening the app does not restore cookies or browsing session.

### Stage 4 — Voice control for a small command set

- Add a push-to-talk or explicit listening toggle; do not keep the microphone open by default.
- Start with Japanese commands for search, back, forward, reload, stop, pause/play, and seek backward/forward.
- Parse speech into a fixed typed command set; do not allow generated arbitrary JavaScript or shell commands.
- Show the recognized command and its target action before or as it runs.
- Keep search/navigation in the browser UI and ensure page-provided text cannot alter the command parser.

**Complete when:** each supported command can be recognized and mapped to its intended browser action, while unknown speech produces no action.

### Stage 5 — Search and result selection

- Support natural-language search requests by converting them to a normal search query or opening search results.
- Let the user choose a result by visible title/position, then open it in the current browser view.
- Require confirmation for actions outside ordinary browsing, including downloads, sign-in, purchases, posting, or submitting forms.

**Complete when:** a spoken topic search can be carried out and the user can select a result without unrestricted page automation.

### Stage 6 — Packaging and release readiness

- Build a Windows package from a clean environment and document installation/startup.
- Check launch behavior, runtime dependencies, microphone permission UX, session cleanup, and YouTube playback in the packaged build.
- Create a third-party notices and dependency-license inventory; resolve Qt, Chromium, codec, model, and packaging-tool redistribution requirements.
- Choose and add the project license only after that review; update repository metadata if needed.
- Add contribution and issue-reporting instructions once the Windows build is reproducible.

**Complete when:** another Windows machine can install and run the package from documented steps, all known limits are recorded, and license/notice files match the shipped dependencies.

## First milestone

Implement only Stages 0 and 1 first. The first visible result is a minimal PySide6 + Qt WebEngine window that opens and loads a page on Windows. Keep the first pass small; defer voice recognition, search-result automation, and packaging polish until the browser shell is confirmed working.
