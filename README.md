# NixOS basic condifuration

This file contains the basis configuration I use after a fresh reinstall of nixos. It adds 'git' and 'vim' in my profile in order to do some basic editing. Also, it activates my bluetooth so that I can add a mouse. Finally, the experimental nixos features flakes is added.

## Instruction to clone this to a fresh install

1. Install git and vim in a temporary shell

``
nix-shell -p git vim
``

2. Keep a copy of your original /etc/nixos directory

``
sudo cp -r /etc/nixos  /etc/nixos-original 
``

3. Clone this repository to your home folder

``
git clone git@github.com:eelcovv/etc-nixos-configuration.git 
``

4. Copy the cloned repository to the etc directory 

``
sudo mv etc-nixos-condifuration /etc/nixos
``

5. Copy the safed hardware-configuration to your new nixos folder
``
cp /etc/nixos-original/hardware-configuration.nix /etc/nixos/hardware-configuration.nix
``

6. Change the ownership of the new nixos folder and its contents. Keep the .git folder intact.
``
sudo chmod root /etc/nixos /etc/nixos/configuration.nix
sudo chgrp root /etc/nixos /etc/nixos/configuration.nix
``

7. *Important*: restore the link to your harddrive in the new configuration.nix based on your stored version. Edit /etc/configuration and replace line 17 with:
``
  boot.initrd.luks.devices."luks-0bb5b2e7...
``
with the version stored in /etc/nixos-original/configuration.nix

8. Rebuild your system and log back in
``
sudo nixos-rebuild switch
``
