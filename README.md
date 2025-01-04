# NixOS basic configuration.nix file

Basis configuration.nix file to use for a fresh reinstall of nixos. It does the following:
1. Add  *git* *vim* and *wget* for basic manipulations 
2. Turn on bluetooth 
3. Add *flakes* to nix 

## Instruction to use

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

4. Move the cloned repository to the etc directory 

``
sudo mv etc-nixos-condifuration /etc/nixos
``

5. Copy the safed hardware-configuration to your new nixos folder

``
cp /etc/nixos-original/hardware-configuration.nix /etc/nixos/
``

6. Change the ownership of the new nixos folder and its contents. Keep the .git folder intact.

``
sudo chmod root /etc/nixos /etc/nixos/configuration.nix
``

and 

``
sudo chgrp root /etc/nixos /etc/nixos/configuration.nix
``

7. *Important*: restore the link to your harddrive in the new configuration.nix based on your stored version. 
Edit line 17 in */etc/configuration.nix* :

``
  boot.initrd.luks.devices."luks-0bb5b2e7...
``

with the line stored in */etc/nixos-original/configuration.nix*

8. Rebuild your system and log back in

``
sudo nixos-rebuild switch
``


Reboot and you should be ready to go
