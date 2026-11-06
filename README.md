# Real-world benchmarks

Well-known open-source projects, built with their own CI steps, on a GitHub-hosted runner and on [Piston](https://piston.sh) at the same time.

Each pull request here runs one project at a fixed commit, three times in parallel: on `ubuntu-latest`, on `piston-2cpu-ubuntu-2402` and on `piston-4cpu-ubuntu-2402`. All three jobs run the same steps and use GitHub's cache. When they finish, the run's summary shows how long each took.

| Language | Project | What runs |
|---|---|---|
| Rust | [Bevy](https://github.com/bevyengine/bevy) | `cargo run -p ci -- test`, Bevy's Linux CI job |
| Java | [Spring Framework](https://github.com/spring-projects/spring-framework) | `./gradlew check antora`, Spring's pull request build |
| JavaScript | [VS Code](https://github.com/microsoft/vscode) | Installing with pnpm, then the compile VS Code's pull request CI runs |

## Reading a run

Open a pull request's checks, then the run's **Summary**. The table there has each runner's CPUs, its whole job, its build step and its cache steps. Under it, each Piston size's time is compared with `ubuntu-latest`'s.

The first run of a workflow fills each runner's cache. Later runs read it, as everyday CI does. To measure again, open **Actions**, pick the workflow and click **Run workflow**.

## Keeping it fair

- GitHub's `ubuntu-latest` has 2 CPUs in a private repository and 4 in a public one. One Piston size always has the same CPUs: `piston-2cpu-ubuntu-2402` while private, `piston-4cpu-ubuntu-2402` once public. The summary says which.
- Every job checks out the same upstream commit and runs the same steps.
- Each runner keeps its own cache, so neither reads what the other saved.

## The projects

The code isn't copied here. Each job checks out the project from its own repository, under its own license: Bevy is MIT or Apache-2.0, Spring Framework is Apache-2.0, and VS Code is MIT.
