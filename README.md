# Reusable GitHub Actions

This repository hosts a collection of reusable GitHub Actions for personal projects.

## Available Actions

- **Hello World** (`hello-world`): Generates a greeting and surfaces it as output `greeting`.
- **PR Author Bot** (`pr-author-bot`): Wraps opencode to auto-draft PRs for assigned issues and respond to change-request reviews with updates and comments.

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

# pr-author-bot example (responds to issue assignment and change-request reviews)
on:
  issues:
    types: [assigned]
  pull_request_review:
    types: [submitted]

jobs:
  pr-author:
    if: github.event_name == 'issues' || (github.event_name == 'pull_request_review' && github.event.review.state == 'changes_requested')
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v6
      - uses: cmraible/actions/pr-author-bot@main
        with:
          model: openai/gpt-5.3-codex
          openai_api_key: ${{ secrets.OPENAI_API_KEY }}
```

## Adding New Actions

Place each action in `<action-name>/action.yml` at the repo root so they can be referenced with `cmraible/actions/<action-name>@ref`.
