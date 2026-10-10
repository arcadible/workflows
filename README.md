<p align="center">
  <a href="https://arcadible.com">
    <img src="https://adn-arcadible.imgix.net/images/i18n/core/www/appicon-512.png?w=256" alt="Arcadible" height="96">
  </a>
</p>

<h1 align="center">Arcadible Workflows</h1>

<p align="center">
  Release your game from GitHub.
</p>

<p align="center">
  <a href="https://developer.arcadible.com/publish/deploying-from-github">Docs</a> ·
  <a href="https://developer.arcadible.com/getting-started">Getting Started</a> ·
  <a href="https://arcadible.com">Arcadible</a> ·
  <a href="https://studio.arcadible.com">Studio</a>
</p>

<br>

A reusable GitHub Actions workflow that builds a release of your game on [Arcadible](https://arcadible.com) from a tagged commit, so anyone who can push can release.

## Usage

Add `.github/workflows/arcadible-release.yml` to your game's repository. Every starter from `arc init` already has it.

```yaml
name: Arcadible Release

on:
  push:
    tags:
      - "arcadible/release/v*"

permissions:
  contents: write

jobs:
  release:
    uses: arcadible/workflows/.github/workflows/release.yml@v1
```

Then, with the [Arcadible GitHub App](https://github.com/apps/arcadible) installed and the repository connected in [Studio](https://studio.arcadible.com), release with the [CLI](https://www.npmjs.com/package/arcadible):

```sh
arc deploy git
```

`arc deploy git` pushes the tag `arcadible/release/v<version>` for your manifest's version, then waits until the release is published or fails, logged in or not.

## What it does

| Step     | What happens                                                                                  |
| -------- | --------------------------------------------------------------------------------------------- |
| Validate | `arc validate`, with the same rules Arcadible uses, and checks that the tag matches `version` |
| Install  | Installs your dependencies from your lockfile, when there's a build                           |
| Build    | `arc build`, which runs your project's build                                                  |
| Pack     | `arc pack`, the same zip `arc deploy` uploads                                                 |
| Release  | Creates a GitHub release with the zip; a prerelease version goes to `staging`                 |

The Arcadible GitHub App picks up the release and publishes it, and its result shows as a check on the tagged commit, in Studio, and by email.

## Learn more

- [Deploying from GitHub](https://developer.arcadible.com/publish/deploying-from-github): setting it up, the check on each release, and when a release doesn't arrive.
- [Releases](https://developer.arcadible.com/publish/releases): where a release's result shows, and how to fix a failed one.
- [The CLI](https://developer.arcadible.com/references/arcadible-cli): every `arc` command.

## License

Apache-2.0
