# Introduction

This repository contains a git post-receive hook for running [r10k](https://github.com/adrienthebo/r10k) via [gitolite3](https://github.com/sitaramc/gitolite). I've only tested it on Fedora 19 with the configuration below.

# Configuration

## _/etc/r10k.yaml_

    # The location to use for storing cached Git repos
    :cachedir: '/var/cache/r10k'

    # A list of git repositories to create
    :sources:
      # This will clone the git repository and instantiate an environment per
      # branch in /etc/puppet/environments
      :puppet:
        remote: 'file:///var/lib/gitolite3/repositories/puppet.git'
        basedir: '/etc/puppet/environments'

    # This directory will be purged of any directory that doesn't map to a
    # git branch
    :purgedirs:
      - '/etc/puppet/environments'

## Permissions

    chown gitolite3:gitolite3 /var/cache/r10k
    chown gitolite3:puppet /etc/puppet/environments
    chown gitolite3:puppet /var/lib/gitolite3/.puppet
    chmod g+s /etc/puppet/environments
    chmod g+s /var/lib/gitolite3/.puppet
