# renovate-config

Shared [Renovate](https://docs.renovatebot.com/) settings for my repos, so the rules live in one place.

## Use it in a repo

`renovate.json` in a repo **without** tests (Renovate opens PRs, you merge them):

```json
{ "extends": ["github>adman234/renovate-config"] }
```

`renovate.json` in a repo **with** tests (minor and patch updates merge themselves once CI passes):

```json
{ "extends": ["github>adman234/renovate-config", "github>adman234/renovate-config:automerge"] }
```

## What the defaults do

- Runs Monday mornings, at most 5 open PRs per repo.
- Each repo gets a **Dependency Dashboard** issue listing every pending update.
- GitHub Actions updates come as one grouped PR and merge automatically.
- torch / torchvision / torchaudio / CUDA images are grouped and never auto-merged.
- Android Gradle Plugin, Kotlin and KSP are grouped and never auto-merged.
- Major updates wait until you tick them on the Dependency Dashboard.

## Tracking versions inside Dockerfiles

Put a `# renovate:` comment above an `ARG` or `ENV` version and Renovate will update it:

```dockerfile
# renovate: datasource=pypi depName=torch
ARG TORCH_VERSION=2.8.0
```

Other datasources work the same way, e.g. `datasource=github-releases depName=owner/repo` or `datasource=git-refs depName=https://github.com/owner/repo`.
