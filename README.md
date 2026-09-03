# GPO Fishing Bot — updates

This repository exists so the app can update itself. It holds two things and
nothing else:

- `latest.json` — which version is current, where to download it, and its
  SHA-256 checksum
- the release archives, attached to each tagged release

There is no source code here. That lives in a private repository.

## How the app uses it

On launch, the app reads `latest.json` over HTTPS. If it names a version newer
than the one installed, it downloads that archive, checks it against the
checksum above, unpacks it beside the current version and switches to it on the
next start. If anything about that fails — no network, a slow server, a
checksum that does not match, an archive with no runnable app inside — it runs
the version already installed and writes the reason to its log.

Versions install side by side and are never overwritten in place, so a release
that will not start is rolled back automatically.
