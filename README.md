# Utility Containers

Containers I use for quick tasks. The containers are built daily to ensure they are up to date.

## Example Usage

Run an Ubuntu container that has common utilities pre-installed:

```bash
docker run --pull --rm -it registry.gitlab.com/gbe0/utility-containers/ubuntu-base:latest
```

## Available Containers

There are multiple containers available with various levels of pre-installed utilities.

### Ubuntu

These containers use Ubuntu as a base image.

#### Base Container

* Container base image: `ubuntu:jammy` (Ubuntu Jammy)
* Container: `registry.gitlab.com/gbe0/utility-containers/ubuntu-base:latest`
* Run container: `docker run --pull --rm -it registry.gitlab.com/gbe0/utility-containers/ubuntu-base:latest`
* Packages added:
  * base-completion
  * curl
  * dig
  * dnsutils
  * iputils-ping
  * jq
  * less
  * mtr
  * neovim
  * net-tools
  * strace
  * tcptraceroute
  * telnet
  * tmux
  * vim
  * wget
  * zsh
  * zsh-completion
* Configuration added:
  * My vimrc
  * My neovimrc
  * My tmux configuration
  * SSH host key checking disabled
  * oh-my-zsh installed
  * Default shell set to zsh
