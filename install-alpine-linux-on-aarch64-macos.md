# Install Alpine Linux on aarch64 macOS

``` yaml
date: 2025-01-20
```

This guide aims to help you install [Alpine Linux] into a [UTM] virtual machine.

[Alpine Linux]: https://alpinelinux.org
[UTM]: https://mac.getutm.app

## Official guide

See [Alpine user handbook] for a complete reference.

[Alpine user handbook]: https://docs.alpinelinux.org/user-handbook/0.1a/index.html

## Download Alpine

[Download Alpine]—Select “Standard aarch64”.

[Download Alpine]: https://alpinelinux.org/downloads/

Verify the integrity of the ISO:

``` sh
shasum -a 256 alpine-standard-3.21.2-aarch64.iso
```

Expected output:

```
8aaf23ac55a0b2576c54d3bb8ad48fe81bd14bdc4def2da2f2d9a8113c66328e
```

## Create the virtual machine

Open UTM.

Create a new virtual machine.

``` yaml
Name: Alpine Linux
Architecture: ARM64 (aarch64)
RAM: 8 GB
Storage: 64 GB
Enable hardware OpenGL acceleration: yes
Enable directory sharing: yes
Boot image: alpine-standard-3.21.2-aarch64.iso
```

Click the “Play” button.

## Set up Alpine

Log in as “root”. No password is required.

``` sh
setup-alpine
```

``` yaml
Select keyboard layout: [none]
Enter system hostname: kanto
Which interface do you want to initialize: [eth0]
IP address for “eth0”: [dhcp]
Do you want to do any manual network configuration: [n]
Choose password for “root”: root
Which time zone are you in: Europe/Paris
HTTP/FTP proxy URL: [none]
Which NTP client to run: [chrony]
Enter APK mirror number or URL: [1]
Set up a user: taupiqueur
Full name for user “taupiqueur”: Mathieu Ablasou
Choose password for “taupiqueur”: taupiqueur
Enter SSH key or URL for “taupiqueur”: [none]
Which SSH server: [openssh]
Which disk would you like to use: vda
How would you like to use it: sys
Erase the above disk and continue: y
```

See [setup-alpine] for details.

[setup-alpine]: https://docs.alpinelinux.org/user-handbook/0.1a/Installing/setup_alpine.html

If everything went well, you should see:
“Installation is complete. Please reboot.”

## Shut down the VM and remove the ISO

``` sh
poweroff
```

Clear CD/DVD.

## Boot “Alpine Linux” and run post-installation tasks

You can use the “taupiqueur” user Alpine Linux created for you
during the installation procedures.

The following sections are all optional.

## Changing your shell

``` sh
apk add bash
chsh -s /bin/bash
```

## Granting your user administrative access

``` sh
apk add doas
```

## Getting a graphical environment

``` sh
setup-desktop
```

See [setup-desktop] for details.

[setup-desktop]: https://docs.alpinelinux.org/user-handbook/0.1a/Working/post-install.html#_getting_a_graphical_environment
