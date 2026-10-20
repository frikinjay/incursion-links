# Incursion community links

Which CurseForge and Modrinth projects are the same mod, decided by the people who link them in
[Incursion](https://github.com/frikinjay/incursion). Incursion uses this file to match projects across the two
platforms, so it needs fewer requests to both sites.

## How it works

- When someone links two projects in Incursion (and hasn't turned sharing off), the app sends an anonymous vote:
  the content type and the two project ids, nothing else. Only Microsoft accounts can vote; the account is
  confirmed by Mojang, and the service keeps only a one-way code of it.
- Once a day the Incursion service counts the votes. A link needs **at least 3 voters and 70% agreement on both
  sides** (5 voters and 80% to change a link that's already published). Every new link is checked against both
  platforms: same content type, and the same project by name and author.
- The result is proposed as a pull request on this repository. **Nothing reaches players until it is merged.**
- `links.json` is signed (`links.json.sig`, Ed25519). Incursion ignores any file whose signature doesn't match the
  key built into the app, so editing `links.json` by hand makes apps reject it.

## links.json

```json
{
  "v": 1,
  "generatedAt": "2026-10-20",
  "links": {
    "mod": [[cfProjectId, "modrinthId", voters, "Name"], ...],
    "resourcepack": [...], "shader": [...], "datapack": [...]
  }
}
```

Each type's list is in alphabetical order of name. A `null` on one side means "not on that platform".

## Leaving something out

Add it to `exclude.json` (merged changes apply from the next daily run):

```json
{
  "pairs": [{ "type": "mod", "cf": 238222, "mr": "u6dRKJwZ" }],
  "projects": [{ "type": "mod", "cf": 12345 }, { "type": "shader", "mr": "abcdefgh" }]
}
```
