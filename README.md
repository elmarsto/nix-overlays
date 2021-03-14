# nix overlays

My (Elmarsto's) nix overlays, forked from [Zanc's nix overlays](https://gitlab.com/zanc/overlays.git).

I'm still new somewhat to NixOS so basically I just pruned what I didn't need and made installation more convenient for my habits

Mostly I just wanted an easier install pattern for Edge.

Currently, it's:

 - Go to [the Microsoft edge-dev Debian Repo](https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-dev/)
 - Download the latest version, whatever it is, to /tmp/edge.deb (right-click, choose "Save as")
 - From this directory, run
  > `nix-env -i -E 'f: with import <nixpkgs> { overlays = import ./overlays.nix; config = { allowUnfree = true; }; }; microsoft-edge-dev'`
