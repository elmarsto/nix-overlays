# nix overlays

My (Elmarsto's) nix overlays, forked from [Zanc's nix overlays](https://gitlab.com/zanc/overlays.git).

I'm still new somewhat to NixOS so basically I just pruned what I didn't need and made installation more convenient for my habits

Mostly I just wanted an easier install pattern for Edge.

Currently, it's:

 - Go to [the Microsoft edge-dev Debian Repo](https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-dev/)
 - Download the latest version, whatever it is, to /tmp/edge.deb (save as)
 - ```bash
nix-env -i -E 'f: with import <nixpkgs> { overlays = import ./overlays.nix; config = { allowUnfree = true; }; }; microsoft-edge-dev'
```
 - Enjoy


## Usage

Add the following to your `/etc/nixos/configuration.nix`:

```nix
{ config, pkgs, options, ... }:

let
  nixpkgs-overlays = builtins.fetchTarball "https://gitlab.com/api/v4/projects/zanc%2Foverlays/repository/archive.tar.gz?sha=master";
in {
  nix.nixPath = options.nix.nixPath.default ++ [ "nixpkgs-overlays=${nixpkgs-overlays}/overlays.nix" ];
  nixpkgs.overlays = import (nixpkgs-overlays + "/overlays.nix");
}
```

To pin, simply change `sha=master` to `sha=0000000000000000000000000000000000000000`.
