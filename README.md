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

# Branching
TODO

# Other links
- https://android.googlesource.com/platform/docs/source.android.com/+/ics-mr1/src/source/using-repo.md
