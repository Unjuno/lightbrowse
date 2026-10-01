# Browser engine and implementation notes

## Decision

- Build a lightweight custom browser shell; do not fork a full browser distribution.
- Initial target: Windows.
- Browser engine: Qt WebEngine (Chromium-based).
- Application language and bindings: Python with the official PySide6 Qt for Python bindings.
- Build separately for each operating system. A Windows binary is not expected to run on macOS or Linux.
- Keep the first version small and verify YouTube search and playback on Windows.

## Data and automation boundaries

- Use an off-the-record Qt WebEngine profile so cookies, cache, and browsing data stay in memory and are discarded when the app exits.
- Do not include a password manager or persist login sessions.
- Add navigation and command restrictions to reduce accidental sign-in or other unintended actions by voice control.
- Treat the profile behavior and supported video playback as items to verify in the first working prototype.

## Licensing status

The repository was initially created with Apache-2.0 selected, and a LICENSE file was added. The project license is now undecided and should be selected after the implementation and dependency inventory are clearer. Before choosing a license, review Qt/PySide6, Qt WebEngine/Chromium, video codecs, and other bundled components and their redistribution terms.
