---
title: Contributing
---

Contributions are welcome, and they are greatly appreciated! Every
little bit helps, and credit will always be given.

You can contribute in many ways:

### Types of Contributions

#### Report Bugs

Report bugs at each individual repository in the `issues` section.

If you are reporting a bug, please include:

* Your operating system name and version.
* Any details about your local setup that might be helpful in troubleshooting.
* Detailed steps to reproduce the bug.

#### Fix Bugs

Look through the GitHub issues for bugs. Anything tagged with "bug"
is open to whoever wants to fix it.

#### Implement Features

Look through the GitHub issues for features. Anything tagged with "feature"
is open to whoever wants to implement it.

#### Write Documentation

Any application could always use more documentation, whether as part of the
official docs, in docstrings, or even on the web in blog posts,
articles, and such.

#### Submit Feedback

The best way to send feedback is to file an issue in the repository `issues` page.

If you are proposing a feature:

* Explain in detail how it would work.
* Keep the scope as narrow as possible, to make it easier to implement.
* Remember that this is a volunteer-driven project, and that contributions
  are welcome :)

#### Add Translations

All translations are handled by [transifex](https://app.transifex.com/nephila/>).

If you want to contribute on translations, request an access to our `transifex` team and we'll add you
as soon as possible.

### Get Started!

Ready to contribute? Refer to the project `Get Started!` section of `CONTRIBUTING.rst`
to set up your environment for local development.

We use, for most projects, this set of packages:

- [bumpversion](https://pypi.org/project/bump2version/)
- [towncrier](https://pypi.org/project/towncrier/#news-fragments)
- [invoke](https://pypi.org/project/invoke/)
- [tox](https://pypi.org/project/tox/)

You may want to install them in the global environment::

    pip3 install --user bump2version towncrier invoke tox

#### Development tips

Most of the projects allows you to use [pre-commit](https://pre-commit.com/) to ensure an easy compliance
to the project code styles.

If you want to use it, install it globally (for example with `pip3 install --user pre-commit`,
but check [installation instruction](https://pre-commit.com/#install>).
When first cloning the project ensure you install the git hooks by running `pre-commit install`.

From now on every commit will be checked against our code style.

Check also the available tox environments with `tox -l`: the ones not marked with a python version number are tools
to help you work on the project buy checking / formatting code style, running docs etc.

#### Testing tips

You can test your project using any specific combination of python, django and django cms (if the project uses django and/or django cms).

For example `tox -epy39-django32-cms39` runs the tests on python 3.7, Django 3.0 and django CMS 3.7.

If the project uses [pytest](https://pytest.org/) as test runner, you can pass any pytest option by setting the
`PYTEST_ARGS` environment variable, usually by prepending to the `tox` command. Example::

    PYTEST_ARGS=" -s  tests/test_plugins.py::PluginTest -p no:warnings" tox -epy37-django30-cms37

### Pull Request Guidelines

Before you submit a pull request, check that it meets these guidelines:

#. Pull request must be named with the following naming scheme:

   `<type>/(<optional-task-type>-)<number>-description`

   See below for available types.

#. The pull request should include tests.
#. If the pull request adds functionality, the docs should be updated.
   Documentation must be added in `docs` directory, and must include usage
   information for the end user.
   In case of public API method, add extended docstrings with full parameters
   description and usage example.
#. Add a changes file in `changes` directory describing the contribution in
   one line. It will be added automatically to the history file upon release.
   File must be named as `<issue-number>.<type>` with type being:

   * `.feature`: For new features.
   * `.bugfix`: For bug fixes.
   * `.doc`: For documentation improvement.
   * `.removal`: For deprecation or removal of public API.
   * `.misc`: For general issues.

   Check `towncrier`_ documentation for more details.

#. The pull request should work for all python / django / django CMS versions
   declared in tox.ini.
   Check the CI and make sure that the tests pass for all supported versions.

### Release a version

Some projects use both `develop` and `master` branches (where `develop` is used for development releases,
and `master` for official releases), other projects use only one branch (`develop` or `master`).
Please refer to the correct workflow between the two below.

#### Projects that use both develop and master branches

#. Update `AUTHORS.rst` file, if preset
#. Merge `develop` on `master` branch
#. Bump release via task: `inv tag-release (major|minor|patch)`
#. Update changelog via towncrier: `towncrier --yes`
#. Commit changelog with `git commit --amend` to merge with bumpversion commit
#. Create tag `git tag <version>`
#. Push tag to github
#. Publish the release from the tags page
#. If pipeline succeeds, push `master`
#. Merge `master` back on `develop`
#. Bump developement version via task: `inv tag-dev -l (major|minor|patch)`
#. Push `develop`

#### Projects that use only develop or master branch

#. Update `AUTHORS.rst` file, if preset
#. Bump release via task: `inv tag-release (major|minor|patch)`
#. Update changelog via towncrier: `towncrier --yes`
#. Commit changelog with `git commit --amend` to merge with bumpversion commit
#. Create tag `git tag <version>`
#. Push tag to github
#. Publish the release from the tags page
#. If pipeline succeeds, push the project main branch (`master` or `develop`)
#. Bump developement version via task: `inv tag-dev -l (major|minor|patch)`
#. Push the project main branch (`master` or `develop`)
