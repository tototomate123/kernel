## Prerequisites

 - [Docker](https://www.docker.com/) for creating our build-environment.
 - [Qemu](https://www.qemu.org/) for emulating our operating system.


## Setup

Build an image for our build-environment:
 - `docker build buildenv -t myos-buildenv`

## Build

Enter build environment:
 - Linux or MacOS: `docker run --rm -it -v "$(pwd)":/root/env myos-buildenv`
 - Windows (CMD): `docker run --rm -it -v "%cd%":/root/env myos-buildenv`
 - Windows (PowerShell): `docker run --rm -it -v "${pwd}:/root/env" myos-buildenv`
 - Please use the linux command if you are using `WSL`, `msys2` or `git bash`

Build for x86 (other architectures may come in the future):
 - `make build-x86_64`
 - If you are using Qemu, please close it before running this command to prevent errors.

To leave the build environment, enter `exit`.


## Emulate

You can emulate your operating system using [Qemu](https://www.qemu.org/): (Don't forget to [add qemu to your path](https://dev.to/whaleshark271/using-qemu-on-windows-10-home-edition-4062#:~:text=2.-,Add%20Qemu%20path%20to%20environment%20variables%20settings,-Copy%20the%20Qemu)!)

 - `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso`
 - `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -d int,guest_errors,cpu_reset -no-reboot -D qemu_log.txt` for some logging into a textfile
 - `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -d int,guest_errors,cpu_reset -no-reboot -D qemu_log.txt -s -S` for logging AND gdb support ( open 2nd terminal, run gdb and connect to qemu via localhost:1234)

