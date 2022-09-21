# Content Move from `ably/docs`

## Overview

On 20 September 2022 this [`textile/` folder](./) was pushed to this repository, along with Git commit history relating only to the files contained within.

## How

All steps carried out by [Quintin Willison](https://github.com/QuintinWillison), exactly as described below...

First, the [git-filter-repo](https://github.com/newren/git-filter-repo) tool was used.
It was installed on local machine (macOS 12.2.1) via Homebrew with:

    brew install git-filter-repo

And then a local, clean clone of the `ably/docs` repository was made in a temporary folder and the tool was run with:

```sh
#!/bin/sh
set -e

git clone git@github.com:ably/docs.git

cd docs

git rev-parse HEAD
git rev-parse --short HEAD

git filter-repo \
    --path content/client-lib-development-guide/ \
    --path-rename 'content/client-lib-development-guide/':'textile/'
```

Generating the following output:

```
Cloning into 'docs'...
remote: Enumerating objects: 44063, done.
remote: Counting objects: 100% (216/216), done.
remote: Compressing objects: 100% (181/181), done.
remote: Total 44063 (delta 73), reused 94 (delta 32), pack-reused 43847
Receiving objects: 100% (44063/44063), 207.69 MiB | 3.30 MiB/s, done.
Resolving deltas: 100% (31958/31958), done.
aa02908896d7af2c95ac08fdaaf6e124ca742a07
aa029088
Parsed 6077 commits
New history written in 1.49 seconds; now repacking/cleaning...
Repacking your repo and cleaning out old unneeded objects
HEAD is now at 7772adbc Merge pull request #1530 from ably/tp4-and-tm3-clarification
Enumerating objects: 4502, done.
Counting objects: 100% (4502/4502), done.
Delta compression using up to 16 threads
Compressing objects: 100% (1275/1275), done.
Writing objects: 100% (4502/4502), done.
Total 4502 (delta 2225), reused 4502 (delta 2225), pack-reused 0
Completely finished after 6.78 seconds.
```

To combine this with this repository, [these instructions](https://jeffkreeftmeijer.com/git-combine/) were used...

Then, from a local up-to-date instance of this repository, a temporary remote was added using:

    git remote add temp-docs ~/code/TEMP/docs

A `git fetch` was run:

    git fetch temp-docs

And the merge commit then created:

    git merge temp-docs/main --allow-unrelated-histories

And then pushed to `origin` (GitHub, this repository).
