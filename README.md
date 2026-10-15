# Rumi apps

This repo is the signed catalog of the Store of [Rumi](https://github.com/surajsaxena123/Rumi). Rumi reads it only when you open the Store or select Check.

The catalog is private for now. A person gets in with an invite: an access key that only reads this repo. They paste the key one time in Rumi, in Settings, under App Store. Later the catalog becomes public, and then no key is needed.

| Folder | What it holds |
|---|---|
| `metadata/` | The signed files of the catalog: the root, the list of apps (targets), the snapshot and the timestamp |
| `targets/<app>/` | The installers of each app (`.rumiapp` files) |

Each app has two signatures: the signature of its publisher, and the signature of this catalog. Rumi checks both, and the size and SHA-256 of each installer, before it installs an app. The catalog uses the four roles of The Update Framework, so a changed, old or frozen catalog fails the check.

The keys of the catalog are not in this repo. The online keys stay in `~/.config/rumi-catalog/keys.json`. The root key stays offline, in its own file (`root-key.json`): only a new root needs it. Before each change, the tool checks this folder as Rumi does, so it never signs a file that somebody changed without the keys. To add an app, use the tool of Rumi:

```
rumi catalog add <this folder> <installer> --shelf code
rumi catalog verify <this folder>
```

Then commit and push. Sign a new timestamp at least each week: `rumi catalog timestamp <this folder>`.

## Invite a person

1. On GitHub, open Settings, Developer settings, Fine-grained tokens, and generate a new token.
2. Repository access: only this repo. Permissions: Contents, read-only. Give it an end date and the name of the person.
3. Send the key to the person in a private way. They paste it in Rumi: Settings, App Store, Save key. Or they run `rumi catalog key`.
4. To end the access of a person, delete their token on GitHub.
