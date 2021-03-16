# SVN - Git migration helper

Creates Vagrant environment with some tools for migrating repositories from Subversion to Git.
Instructions can also be used without Vagrant to migrate repositories.

## Usage

Build and start virtual machine by running
`vagrant up`

Connect to vm by `vagrant ssh`

## Migration

VM has following tools installed:
- git
- svn
- git-svn
- svn2git

Svn2git makes migration easier by automating some git-svn tasks like creating branches for you.

svn2git instructions can be found in [https://github.com/nirvdrum/svn2git]

Migration environment should have case sensitive file system to prevent corruption while migrating.
This Vagrant environment has case sensitive file system but I suggest that migration is run in other location than /vagrant which is shared to host system.
If you want to visualise repository after migration, it is safe to move migrated repository folder to /vagrant where it can be accessed in the host system.

### Getting SVN authors
`svn log -q https://svn.example.com/repository_name | awk -F '|' '/^r/ {sub("^ ", "", $2); sub(" $", "", $2); print $2" = "$2" <"$2">"}' | sort -u > authors.txt`

### Show files over 2M in git history
`git rev-list --objects --all | git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' | sed -n 's/^blob //p' | sort --numeric-sort --key=2 | cut -c 1-12,41- | awk '$2 >= 2^20' | $(command -v gnumfmt || echo numfmt) --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest`

### Show 20 largest files in current folder
`du -a . | sort -n -r | head -n 20`

### Remove files from git history
https://help.github.com/en/articles/removing-sensitive-data-from-a-repository
