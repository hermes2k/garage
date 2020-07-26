
# Preparing a Pull Request

After adding a new feature or implementing a bug fix, you will probably want to
merge your fix into the garage master branch and make it available to others.
This page will guide you through the process of creating a pull request and
merging your changes.

## Precursors

Assuming you read and followed the [git workflow](git_workflow.md) guide,
you're almost ready to submit a PR. You should make sure your feature branch is
rebased on to the latest version of `rlworkgroup/master` and that your
pre-commit hooks pass, then run the test suite as shown below.

### Passing the Test Suite

Before submitting a PR, you should make sure that your changes do not cause any
breakages in the garage codebase. We do this by running the test suite, which
includes all the unit and integration tests that exist on the master branch,
plus any new ones you added. You can run the test suite locally from the garage
root directory by running

```sh
make test
```

This will run the test suite in a docker container, so be sure to have docker
installed.

## Submitting a PR

Once you've completed the above steps, you are ready to submit a PR. First push
your updated feature branch to your github fork:

```sh
git push origin your-feature-branch
```

Then, navigate to your github fork, switch to your feature branch, and click on
`pull-request`.  On the next page, select `rlworkgroup/garage` as the base
repository and your feature branch as the head repository. This will submit a
PR to merge your changes into the base repository. If the changes shown look
good, you can submit your PR.

## Managing a PR

### Passing the Checks

After submitting a PR, you should check to make sure all the required checks
pass. These checks include a CI, which runs the garage test suite, and a Codecov
test, which checks that your code meets the minimum required code coverage
threshold.

If any of the tests in the test suite fail, navigate to the Travis CI run for
your PR by clicking on that test. The CI will include a log that specifies which
tests failed, along with the stacktrace corresponding to the issue.

In some cases, tests on external PRs fail due to access limitations that prevent
some tests from running. If your code coverage percentage is inexplicably low,
mention this in a comment on your PR page.

### Merge Conflicts

If there are merge conflicts between your incoming commits and the master
branch, Github will point them out to you at the bottom of the PR page. If these
conflicts are simple, you can usually address them without having to rebase and
update your PR by using the mergify bot. Submit a comment to your PR with the
following:

```sh
@Mergifyio rebase
```

This invokes the bot and will attempt to do a rebase. If this fails, you will
have to rebase manually on your local and update your fork.

----

*This page was authored by Mishari Aliesa ([@maliesa96](https://github.com/maliesa96)).*
