# kitchen-salt
A Test Kitchen Provisioner for Salt

The provider works by generating a salt-minion config, creating pillars based on attributes in .kitchen.yml & calling salt-call.

This provider has been tested against the Ubuntu boxes running in vagrant/virtualbox & vagrant-lxc boxes on Ubuntu.

## Installation & Setup
You'll need the test-kitchen & kitchen-salt gem's installed in your system, along with kitchen-vagrant or some ther suitable driver for test-kitchen.  Please see the [INTRODUCTION](https://github.com/simonmcc/kitchen-salt/blob/master/INTRODUCTION.md).

## Catching salt failures
Catching salt failures is particularly troublesome, as salt & salt-call don't do a very good job of setting the exit
code to something useful, around ~0.17.5, the `--retcode-passthrough` option was added, but even in 2014.1.0 this is
still flawed, [PR11337](https://github.com/saltstack/salt/pull/11337) should help fix some of those problems.  In the
mean time, we scan the salt-call output for signs of failure (essentially `grep -e Result.*False -e Data.failed.to.compile -e
No.matching.sls.found.for`) and check for a
non-zero exit code from salt-call.


## Requirements
You'll need a driver box that is supported by both the SaltStack [bootstrap](https://github.com/saltstack/salt-bootstrap) system & the Chef Omnibus installer (the Chef Omnibus installer is only needed to provide busser with a useable ruby environment, you can tell busser to use an alternative ruby if your box has suitable ruby support built in).

## Releasing

    # hack. work. test.
    git add stuff
    gem bump --no-commit
    git add lib/kitchen-salt/version.rb
    git commit -v
    git push
    gem release


