# damurka.r-universe.dev

The registry of https://damurka.r-universe.dev: the list of R packages r-universe builds and publishes for this
account. r-universe turns each listed GitHub repo into ready-made binary packages (Windows, macOS, Linux) that install
with plain `install.packages()` -- no compiling, no Rtools, no GitHub token. DataSuite installs the Countdown apps from
here.

| Package | Repo | What |
| --- | --- | --- |
| datasuite.ui | [damurka/datasuite.ui](https://github.com/damurka/datasuite.ui) | DataSuite's Shiny interface kit, chart options and report builder |
| cd2030.core | [damurka/cd2030.core](https://github.com/damurka/cd2030.core) | Countdown to 2030 analysis, datasets and shared pages |
| cd2030.rmncah | [damurka/cd2030.rmncah](https://github.com/damurka/cd2030.rmncah) | the RMNCAH app |
| cd2030.vaxx | [damurka/cd2030.vaxx](https://github.com/damurka/cd2030.vaxx) | the Vaxx (immunization) app |
| cd2030.pooled | [damurka/cd2030.pooled](https://github.com/damurka/cd2030.pooled) | the Pooled app |
| khisr | [damurka/khisr](https://github.com/damurka/khisr) | an R client to retrieve data from DHIS2 |
| kpp2019 | [damurka/kpp2019](https://github.com/damurka/kpp2019) | Kenya population projections 2019 |

How the Countdown packages fit together and how a release reaches DataSuite users:
[countdown-analytics/docs/ARCHITECTURE.md](https://github.com/damurka/countdown-analytics/blob/main/docs/ARCHITECTURE.md).

## Install

```r
install.packages("cd2030.rmncah", repos = c("https://damurka.r-universe.dev", "https://cloud.r-project.org"))
cd2030.rmncah::run_app()
```

The Bayesian coverage packages cd2030.core suggests come from another universe: add
`"https://alkemalab.r-universe.dev"` to `repos`.

## packages.json

One entry per package: its name (must equal `Package:` in the repo's DESCRIPTION) and its git URL.

```json
[
  { "package": "cd2030.core", "url": "https://github.com/damurka/cd2030.core" }
]
```

r-universe also accepts optional keys -- `"branch"` (default: the repo's default branch) and `"subdir"` (a package not
at the repo root); see r-universe's documentation before relying on them.

**To add a package:** add its entry and push. r-universe picks up the change and builds it. **To remove one:** delete
its entry; r-universe stops publishing it.

## When does a package build?

- r-universe watches every listed repo and builds a package when its default branch gets a new commit -- the version
  number doesn't have to change. With the **r-universe GitHub app** installed on the account
  (https://github.com/apps/r-universe), a push starts a build within minutes; without it, r-universe only notices on
  its periodic scan (about hourly, sometimes slower).
- A push to this registry repo makes r-universe re-sync every package listed.
- The builds run as GitHub Actions in [r-universe/damurka](https://github.com/r-universe/damurka/actions) ("Build
  package", one run per package, named after the commit r-universe made there: `<package> <version>`).

## Checking a build

| | |
| --- | --- |
| Dashboard | https://damurka.r-universe.dev/builds -- every package, its version, commit and per-platform check result; signed in with GitHub it has a Rebuild button |
| API | https://damurka.r-universe.dev/api/packages -- `RemoteSha` is the commit that was built; compare it with the repo's `main` |
| Logs | `gh run list -R r-universe/damurka` and `gh run view <id> -R r-universe/damurka --log-failed` |

A failing `R CMD check` on one platform still publishes the package, but fix it: it is what a user of that platform
will hit.
