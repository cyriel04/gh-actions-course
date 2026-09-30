# GitHub Actions Course

Hands-on exercises for learning GitHub Actions. Each workflow in [`.github/workflows`](.github/workflows) covers one concept, and they build on each other from basic jobs and steps up to inputs, environments, and job dependencies.

## Workflows

| #  | Workflow | Trigger | What it covers |
| -- | -------- | ------- | -------------- |
| 01 | [Building Blocks](.github/workflows/01-building-blocks.yaml) | `workflow_dispatch` | Workflows, jobs, steps, `run` vs `uses` |
| 02 | [Workflow Events](.github/workflows/02-workflow-events.yaml) | `workflow_dispatch` | Event triggers, `github.event_name`, `github.actor` |
| 03 | [Workflow Runners](.github/workflows/03-workflow-runners.yaml) | `workflow_dispatch` | Ubuntu, Windows, and macOS runners, `$RUNNER_OS`, `shell` |
| 04 | [Using Actions](.github/workflows/04-using-actions.yaml) | `workflow_dispatch` | `actions/checkout`, `actions/setup-node`, `working-directory`, running a React app's tests |
| 05 | [Event Filters & Activity Types](.github/workflows/05-1-filters-activity-types.yaml) | `pull_request` | Filtering by activity `types` and `branches` |
| 06 | [Contexts](.github/workflows/06-contexts.yaml) | `workflow_dispatch` | The `github` and `vars` contexts |
| 07 | [Expressions](.github/workflows/07-expressions.yaml) | `workflow_dispatch` | `${{ }}` expressions, `run-name`, conditional steps with `if` |
| 08 | [Variables](.github/workflows/08-variables.yaml) | `workflow_dispatch` | `env`, repository variables, environment-scoped variables |
| 09 | [Functions](.github/workflows/09-functions.yaml) | `workflow_dispatch` | `toJson()`, status functions `success()` and `failure()` |
| 10 | [Execution Flow](.github/workflows/10-execution-flow.yaml) | `workflow_dispatch` | Job dependencies with `needs`, failing a job on purpose |
| 11 | [Inputs](.github/workflows/11-inputs.yaml) | `workflow_dispatch` | `boolean`, `choice`, and `environment` inputs, dynamic environments |

## Repository layout

```
.
├── .github/workflows/        # One workflow per lesson
└── 04-using-actions/
    └── react-app/            # Create React App (TypeScript) used by workflow 04
```

## Running the workflows

Most workflows use `workflow_dispatch`, so you run them by hand:

1. Open the **Actions** tab of the repository.
2. Pick a workflow from the sidebar.
3. Click **Run workflow**, fill in any inputs, and start it.

With the [GitHub CLI](https://cli.github.com/):

```sh
gh workflow run "11 - Working with Inputs" -f target-environment=staging -f tag=v2.0
gh run watch
```

Workflow 05 runs on its own when a pull request targeting `main` is opened or updated.

## Required setup

Some lessons read variables and environments that you need to create in **Settings**:

| Name | Kind | Used by |
| ---- | ---- | ------- |
| `MY_VAR` | Repository variable | 06, 08 |
| `staging` | Environment | 08, 11 |
| `STAGING_VAR` | Variable on the `staging` environment | 08 |

Workflow 11 lists whatever environments exist in the repository, so add more (for example `production`) if you want to deploy to them.

## Running the React app locally

```sh
cd 04-using-actions/react-app
npm ci
npm test
npm start
```
