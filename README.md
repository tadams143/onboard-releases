# Onboard releases

Signed releases of **Onboard**, the guest and crew information app for yachts. This repository holds only the
release files that vessels download; the source is kept elsewhere.

Each [release](../../releases) has two files:

| File | What it is |
|---|---|
| `onboard-<version>.tar.gz` | The app: server, front end and updater, ready to install. |
| `latest.json` | The release's manifest (version, date, size, SHA-256, what's new), signed by the supplier. |

## How vessels use it

A vessel's server checks
`https://github.com/tadams143/onboard-releases/releases/latest/download/latest.json` once a day. When a newer
version is out and the vessel has a valid licence key, the admin shows it under **Settings › Updates**. Nothing is
installed until an admin presses **Update now**. The server then:

1. checks that the manifest is signed with the supplier's key (a release signed by anyone else is refused);
2. downloads the bundle and checks its size and SHA-256 against the signed manifest;
3. keeps a copy of the version running now, so **Roll back** can return to it;
4. installs the new version, restarts the app and checks that it comes back, putting the earlier version back if
   it doesn't.

Installing Onboard on a new vessel, and setting up the updater, is covered by the installation guide that comes
with the app (`INSTALL.md`).

## Publishing (supplier only)

Releases are made with `npm run release -- --yes` from the source repository. It builds and signs the bundle and
creates the GitHub release here. Don't upload or edit files here by hand: a changed file no longer matches its
signature, and vessels refuse it.
