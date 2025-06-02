# Renovate Bot Presets

Collection of presets for [Renovate Bot](https://docs.renovatebot.com/).

Renovate Bot automatically updates dependencies. In our experience, it is more
reliable and has better configuration options than Dependabot.

## How to use the presets

To use one of the presets, save a `renovate.json` file with the following
content in the root folder of your Github repository:

```json
{
  "$schema": "https://docs.renovatebot.com/renovate-schema.json",
  "extends": ["github>scoville/renovate-presets:elixir-app"]
}
```

In this example, the preset would be loaded from `elixir-app.json`.

Add the [Renovate app](https://github.com/apps/renovate) to your repository.

You can extend and override the configuration as needed.

### Set reviewers

Set the reviewers to the team that is responsible for the repository.

```json
{
  "reviewers": ["team:myteam"]
}
```

### Ignore Docker container updates

Ignore updates for Docker containers where the version should match the one used
in production (e.g. Postgres, RabbitMQ, Redis).

```json
{
  "ignoreDeps": ["postgres"]
}
```

### Selectively enable managers (optional)

Renovate enables most managers by default. You can enable experimental managers
or selectively enable the managers you need.

```json
{
  "enabledManagers": [
    "docker-compose",
    "dockerfile",
    "github-actions",
    "mix",
    "npm"
  ]
}
```

## Available presets

| Preset name    | Description                        |
| -------------- | ---------------------------------- |
| elixir-app     | Preset for Elixir applications     |
| elixir-library | Preset for shared Elixir libraries |
| terraform      | Preset for Terraform repositories  |

## Adding and updating presets

- Use the suffix `-app` or `-library`, if applicable.
- Add the preset to the "Available presets" section in the readme.
- Remember that this repository is public. Don't expose internals.
- Format all files with `prettier . --write`

### Recommendations for all presets

- Time zone: Asia/Tokyo
- Schedule: Monday to Friday, 09:00-17:00
- For applications: range strategy `pin`
- For libraries: range strategy `widen` (dev dependencies: `pin`)
- For applications: extend `config:best-practices`
- For libraries: extend `config:recommended`
- Enable lock file maintenance
- Enable automerge for dev dependencies
- Set up groups for common related libraries
