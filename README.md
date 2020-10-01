# Repo (git-repo) Example Manifest
This is an example manifest for Google's git-repo tool. Use this to get started
learning about git-repo.

It describes a project consisting of two git repos (not git-repo):

    github.com/tompreston/notes
    github.com/tompreston/dotfiles

# Walk-through
Start by reading the git-repo home page:

    https://gerrit.googlesource.com/git-repo/

Which tells you to install the repo wrapper script:

    curl https://storage.googleapis.com/git-repo-downloads/repo > ~/.bin/repo
    chmod a+rx ~/.bin/repo

Then read the command reference:

    https://source.android.com/setup/develop/repo

And learn about the manifest document format:

    https://gerrit.googlesource.com/git-repo/+/master/docs/manifest-format.md

Write the manifest (this repo).

Then create a clean working directory, init .repo and sync:

    mkdir wd
    cd wd
    repo init -u https://github.com/tompreston/repo-example-manifest
    repo sync

At the init stage, the `repo` wrapper will first download git-repo itself, then
the manifest. Sync will pull the projects.

Run `repo` and `repo help` to learn more about git-repo commands:

    repo
    repo help branch

# Branching
Start a new branch called "add-comments" in all projects (or glob):

    $ repo start tpreston/repo-example-add-comments dotfiles notes
    $ repo start tpreston/repo-example-add-comments *

    $ repo branch
    * tpreston/repo-example-add-comments | in all projects

And in each project (default: all), we can see the new branch:

    $ repo forall dotfiles notes -c 'git branch'
    $ repo forall -c 'git branch'
    * tpreston/repo-example-add-comments
    * tpreston/repo-example-add-comments

Make some changes and view them:

    vim dotfiles/README.md notes/README.md
    repo diff
    repo status
    repo info

At this point, it's also worth noting that repo has set up the remote we
specified in the manifest:

    $ repo forall -c 'git remote -v'
    github-ssh      ssh://git@github.com/tompreston/dotfiles (fetch)
    github-ssh      ssh://git@github.com/tompreston/dotfiles (push)
    github-ssh      ssh://git@github.com/tompreston/notes (fetch)
    github-ssh      ssh://git@github.com/tompreston/notes (push)

Batch commit the changes and push to this remote using `$REPO_REMOTE`:

    repo forall -c 'git commit -m "repo-example: Add comments" README.md'
    repo forall -c 'git push $REPO_REMOTE HEAD'

The `repo upload` command only works when we have specified a `review` URL in
the `remote` element in the manifest. It's for gerrit, which I won't go into
here.


# Other links
- https://android.googlesource.com/platform/docs/source.android.com/+/ics-mr1/src/source/using-repo.md
