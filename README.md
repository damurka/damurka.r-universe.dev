# damurka.r-universe.dev

The registry of the packages published at https://damurka.r-universe.dev: DataSuite's interface package
(datasuite.ui), the Countdown to 2030 analysis package (cd2030.core) and the Countdown apps (cd2030.rmncah,
cd2030.vaxx, cd2030.pooled), and khisr and kpp2019. r-universe builds each from its repository's default branch on every push.

Install an app (with its dependencies) from R:

    install.packages("cd2030.rmncah", repos = c("https://damurka.r-universe.dev", "https://cloud.r-project.org"))
    cd2030.rmncah::run_app()
