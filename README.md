# \<Repo Name>

![MkDocs Deployment Status](https://github.com/rowland007/template-repository/actions/workflows/mkdocs.yml/badge.svg)  [![GitKraken Shield](https://img.shields.io/badge/Made%20With-GitKraken%20Git%20Tools-teal?style=plastic&logo=gitkraken)](https://www.gitkraken.com/invite/54HeFuDe)

[\<Repo Name>](https://rowland007.github.io/template-repository/) by [Randall Rowland](https://randyrowland.me) is licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/?ref=chooser-v1) <img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/cc.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/by.svg?ref=chooser-v1"><img style="height:22px!important;margin-left:3px;vertical-align:text-bottom;" src="https://mirrors.creativecommons.org/presskit/icons/nc.svg?ref=chooser-v1">

# Overview

A repository template copies all of its settings and content over to newly created repositories in that project. Utilizing this feature allows users to manage settings centrally & ensure that your repositories are always correctly configured. There is no need to define certain settings all over again. It includes branches and file (README, LICENSE, .gitignore, and .github/workflows) in the template repository every new repository will automatically have. The feature will mirror the content from the template to the new repositories.

# Configuration

## Files

This repository includes the following files

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing](CONTRIBUTING.md)
- [License](LICENSE.md)
- [Readme](README.md)

- [Github Workflow](.github/workflows/ci.yml)
    - This workflow watches the master branch and every time a commit is made, it uses the [mkdocs.yml](mkdocs.yml) file and the `docs/` folder to build mkdocs static website and deploy the repos documentation to the `gh-pages` branch automatically. The documentation can then be viewd at `https://<username>.github.io/<repo-name>/`. For example, this repo's documentation is located at [https://rowland007.github.io/template-repository/](https://rowland007.github.io/template-repository/).

## Branches

This repository initializes two branches, `master` and `develop`.

# Benefits

:white_check_mark: Spend less time repeating code   
:white_check_mark: Focus on building new things   
:white_check_mark: Less manual configuration   
:white_check_mark: Sharing boilerplate code across codebase   
:white_check_mark: Every template has a new url endpoint called **/generate**   
