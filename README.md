# any-nix-shell

`fish` and `zsh` support for the `nix run` and `nix-shell` environments of the Nix package manager.

Features:

* When entering a `nix run` or `nix-shell` environment, the shell stays the same.
* Inside those environments, your prompt prints the loaded packages to the right.
* Alternatively, print that information by executing: `nix-shell-info`
* `nix-shell --command` or the like still execute inside `bash`, such that scripts don't break.

## Installation

any-nix-shell can currently be installed from the official `nixos-unstable` channel
([Link 1](https://www.reddit.com/r/NixOS/comments/7p83y4/install_a_package_from_unstable_while_running/), [Link 2](https://stackoverflow.com/questions/41230430/how-do-i-upgrade-my-system-to-nixos-unstable)).
If you don't know how to do that, you can alternatively execute

```shell
nix-env -i any-nix-shell -f https://github.com/NixOS/nixpkgs/archive/master.tar.gz
```

which installs `any-nix-shell` into your user environment.

## Enabling

In the following we describe how to enable the `any-nix-shell` plugin
for your user.
This differs slightly between `fish` and `zsh`.

### `fish`

Add the following to your *~/.config/fish/config.fish*.
Create it if it doesn't exist.

```fish
any-nix-shell fish --info-right | source
```

### `zsh`

Add the following to your *~/.zshrc*.
Create it if it doesn't exist.

```zsh
any-nix-shell zsh --info-right | source /dev/stdin
```

## System-wide enabling on NixOS

Alternatively the `any-nix-shell` plugin can be enabled system-wide.
This enables it for every user.
To do so, add the following to your configuration (*/etc/nixos/configuration.nix*).

### `fish`

```nix
  programs.fish.enable = true;
  programs.fish.promptInit = ''
    any-nix-shell fish --info-right | source
  '';
```

### `zsh`

```nix
  programs.zsh.enable = true;
  programs.zsh.promptInit = ''
    any-nix-shell zsh --info-right | source /dev/stdin
  '';
```

### `zsh` with home-manager

```nix
  programs.zsh.enable = true;
  programs.zsh.initExtra = ''
    any-nix-shell zsh --info-right | source /dev/stdin
  '';
```

## Customization

The `any-nix-shell` command (which is used for enabling the plugin in a specific shell) **optionally** takes any of the following flags:

| Flag | Description |
| - | - |
| `--info-right` | While in a `nix shell` or `nix-shell` environment, display information about the loaded packages at the right. |
