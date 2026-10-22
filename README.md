# Public update feed

The launcher source repository can stay private. Create a separate public GitHub repository named `KronaLauncher-Updates` for the files that players' launchers must download. The launcher downloads them in the background; it does not open GitHub in a browser.

## Initial setup

1. Create `KarlosR98/KronaLauncher-Updates` as a **public** repository.
2. Copy `updates/events.json` to the root of its `main` branch.
3. Copy `EVENTOS/NigthmareLand/nightmareland_logo.png` to `events/nightmareland.png`.
4. Create a **pre-release** tagged `event-nightmareland-1.0.0` and upload `EVENTOS/NigthmareLand/modsacto1.zip` as `mods.zip`. Keep event-package releases as pre-releases so they do not replace the latest stable launcher release.
5. Create a fine-grained GitHub token that can publish releases in `KronaLauncher-Updates`. Add it to the private launcher repository's Actions secrets as `KRONA_UPDATES_TOKEN`.
6. Publish the first launcher version from the launcher repository using a tag matching the version in `package.json` (for example, `v1.0.0`). The workflow builds the Windows installer and publishes it to the public updates repository.
7. Install that first generated installer on each player's computer. Subsequent launcher releases can then update automatically.

The example event manifest already contains the SHA-256 and size of the current NightmareLand mod ZIP. If the ZIP changes, update both values and the release URL before publishing the new package.

## Adding or updating an event

Upload the event's logo under `events/` and its mod ZIP as an asset in a **pre-release**. Add an entry to `events.json` using a unique lowercase `id`, a Minecraft version, Forge version, server address, HTTPS logo URL, and package URL, SHA-256, and byte size. Commit the updated manifest to the public repository's `main` branch. The launcher refreshes the event list when players open Events and downloads a changed package when they press Play.

Do not put Microsoft tokens, passwords, or private server credentials in this public repository or its releases.
