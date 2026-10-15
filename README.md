# Rumi apps

This repo is the signed catalog of the Store of Rumi. Rumi reads it only when you open the Store or select Check.

The catalog is public: each Rumi reads it with no key.

| Folder | What it holds |
|---|---|
| `metadata/` | The signed files of the catalog: the root, the list of apps (targets), the snapshot and the timestamp |
| `targets/<app>/` | The installers of each app (`.rumiapp` files) |

Each app has two signatures: the signature of its publisher, and the signature of this catalog. Rumi checks both, and the size and SHA-256 of each installer, before it installs an app. The catalog uses the four roles of The Update Framework, so a changed, old or frozen catalog fails the check.

Each signature is quantum-safe: each key of a publisher and each role of the catalog has an ed25519 key and an ML-DSA-65 key (FIPS 204), and Rumi needs a good signature of both. A quantum computer that breaks ed25519 still cannot forge an app or the catalog.

The keys of the catalog are not in this repo. The online keys stay in `~/.config/rumi-catalog/keys.json`. The root keys stay offline, in their own file (`root-key.json`): only a new root needs them. Before each change, the tool checks this folder as Rumi does, so it never signs a file that somebody changed without the keys. To add an app, use the tool of Rumi:

```
rumi catalog add <this folder> <installer> --shelf code
rumi catalog verify <this folder>
```

Then commit and push. Sign a new timestamp at least each week: `rumi catalog timestamp <this folder>`.
