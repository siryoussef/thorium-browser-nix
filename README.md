# Thorium Browser for Nix 

Nix flake for Thorium Browser

This package is meant to be used until the official package is available in nixpkgs. See [progress](https://github.com/NixOS/nixpkgs/pull/261718)

# Usage 

```nix
# flake.nix

{
  inputs.thorium-browser.url = "git+https://codeberg.org/Tomkoid/thorium-browser-nix";
  # ...

  outputs = {nixpkgs, ...} @ inputs: {
    nixosConfigurations.HOSTNAME = nixpkgs.lib.nixosSystem {
      specialArgs = { inherit inputs; }; # this is the important part
      modules = [
        ./configuration.nix
      ];
    };
  } 
}

# configuration.nix

{inputs, pkgs, ...}: {
  # ...
  environment.systemPackages = [
    inputs.thorium-browser.defaultPackage.${system}
  ];
  # ...
}
```
