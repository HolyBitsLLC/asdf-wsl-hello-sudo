# asdf-wsl-hello-sudo

[asdf](https://asdf-vm.com/) plugin for installing [WSL-Hello-sudo](https://github.com/nullpo-head/WSL-Hello-sudo).

WSL-Hello-sudo is a Linux PAM module that lets you authenticate `sudo` via
Windows Hello (face recognition, fingerprint, or PIN) on Windows Subsystem for
Linux.

## Usage

```bash
asdf plugin add wsl-hello-sudo https://github.com/HolyBitsLLC/asdf-wsl-hello-sudo.git
asdf install wsl-hello-sudo latest
asdf global wsl-hello-sudo latest
```

After installation, run the interactive installer to configure the PAM module:

```bash
wsl-hello-sudo-install
```

This invokes the upstream `install.sh` which:

1. Copies a Windows CLI app to `C:\Users\<you>\pam_wsl_hello\`
2. Installs the PAM module into your WSL distribution
3. Creates config files in `/etc/pam_wsl_hello/`
4. Creates a `pam-configs` entry for automatic PAM configuration
5. Generates an `uninstall.sh` you can run later

## Windows-side component path

The installer places its Windows Hello bridge executable on the Windows filesystem.
By default, the path is:

```
C:\Users\<you>\AppData\Local\Programs\wsl-hello-sudo
```

From WSL this is accessible at:

```
/mnt/c/Users/<you>/AppData/Local/Programs/wsl-hello-sudo
```

The PAM module configuration in `/etc/pam_wsl_hello/config` references this
path so it can invoke the Windows Hello prompt from within WSL.

## Plugin scripts

- `bin/list-all` — Lists available versions from GitHub releases.
- `bin/latest-stable` — Prints the latest stable version.
- `bin/download` — Downloads the release tarball for a given version.
- `bin/install` — Extracts the release and installs wrapper commands.
