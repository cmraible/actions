# Reusable GitHub Actions

This repository hosts a collection of reusable GitHub Actions for personal projects.

## Available Actions

- **Hello World** (`hello-world`): Generates a greeting and surfaces it as output `greeting`.

## Usage

```yaml
jobs:
  greet:
    runs-on: ubuntu-latest
    steps:
      - uses: cmraible/actions/hello-world@main
        id: hello
        with:
          name: Octocat
      - run: echo "The action said: ${{ steps.hello.outputs.greeting }}"
```

## Adding New Actions

Place each action in `<action-name>/action.yml` at the repo root so they can be referenced with `cmraible/actions/<action-name>@ref`.
