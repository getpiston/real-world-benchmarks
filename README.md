# Real-world benchmarks

Well-known open-source projects, built with their own CI steps, on a GitHub-hosted runner and on [Piston](https://piston.sh) at the same time.

Each pull request here runs one project at a fixed commit, twice in parallel: once on `ubuntu-latest` and once on `piston-4cpu-ubuntu-2402`. Both jobs run the same steps and use GitHub's cache. When both finish, the run's summary shows how long each took.

| Language | Project | What runs |
|---|---|---|
| Rust | [Bevy](https://github.com/bevyengine/bevy) | `cargo run -p ci -- test`, Bevy's Linux CI job |
| Java | [Spring Framework](https://github.com/spring-projects/spring-framework) | `./gradlew check antora`, Spring's pull request build |
| JavaScript | [VS Code](https://github.com/microsoft/vscode) | Installing with pnpm, then the compile VS Code's pull request CI runs |

## Reading a run

Open a pull request's checks, then the run's **Summary**. The table there has each runner's whole job, its build step and its cache steps.

The first run of a workflow fills each runner's cache. Later runs read it, as everyday CI does. To measure again, open **Actions**, pick the workflow and click **Run workflow**.

## Keeping it fair

- In a public repository, GitHub's `ubuntu-latest` has 4 CPUs, the same as `piston-4cpu-ubuntu-2402`.
- Both jobs check out the same upstream commit and run the same steps.
- Each runner keeps its own cache, so neither reads what the other saved.

## The projects

The code isn't copied here. Each job checks out the project from its own repository, under its own license: Bevy is MIT or Apache-2.0, Spring Framework is Apache-2.0, and VS Code is MIT.
