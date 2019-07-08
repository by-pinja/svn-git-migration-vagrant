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
