# CONTRIBUTING.md

This document must always start by thanking contributors and readers for their interest in contributing to and exploring the repository. It must also set an expectation about how long it will take to review and resolve a contribution, even if that is a long time. The expectation must be realistic, so if the maintainers are students, state that the time is not fixed and can be very long because of their academic workload.

Open with something along the lines of "Thank you so much for taking the time to read this. It genuinely means a lot. {{PROJECT_NAME}} is a small project born at {{HACKATHON_NAME}}, and the fact that you are here considering contributing to it is something we do not take for granted". If the chosen documentation language is not English, translate it following [localization.md](localization.md).

It must explain the dependencies and build steps one by one, covering fork, descriptive branch, clean build and merge by >= 1 maintainer.

On coding standards: derive the style from the project's existing code (a formatter or linter that is already configured — .editorconfig, prettier, black, clang-format...). If there is none, propose the language's own standard (PEP 8, gofmt, Prettier with defaults...) instead of imposing an arbitrary one. It must also include the conventional commits structure, explained later, and the DCO sign-off if it was adopted (`git commit -s`).

It covers how to set up the environment, coding standards, tests, the PR process, commit conventions and review expectations. It defines the "definition of done" for contributions.
