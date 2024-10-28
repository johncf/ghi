# Github Release Installer

A single python script to download, extract and install (read "copy to `$HOME/.local/bin`") pre-built binaries from Github releases.

## Requirements

* Python 3.10+
* Python [`requests` package](https://pypi.org/project/requests/)
  * Note: This is [often](https://packages.debian.org/bookworm/python3-requests) [already](https://packages.ubuntu.com/noble/python3-requests) [installed](https://archlinux.org/packages/extra/any/python-requests/) as a system package.
* (optional) `wget` or `curl`
  * Note: if neither is available, uses `requests` to download (which may be slower and not so robust)

## Installation

1.  Copy [this script](./ghi) to `$HOME/.local/bin`.

1.  Ensure executable permissions:

    ```sh
    chmod +x $HOME/.local/bin/ghi
    ```

1.  Also ensure that `$HOME/.local/bin` is in your `$PATH`. If not, add it:

    ```sh
    SHELL_RC="$HOME/.bashrc"
    echo >> $SHELL_RC
    echo 'export PATH="$PATH:$HOME/.local/bin"' >> $SHELL_RC
    ```

## Usage

```sh
ghi --help
ghi get --help
ghi ls --help
ghi clean --help
```

To download and install the latest release:

```sh
ghi get burntsushi/ripgrep
```

To list last 30 releases:

```sh
ghi ls burntsushi/ripgrep
```

To clean-up cached files:

```sh
ghi clean
```

To change the install target location:

```sh
GHI_TARGET_DIR="$HOME/mybin" ghi get burntsushi/ripgrep
# or
ghi --target-dir "$HOME/mybin" get burntsushi/ripgrep
```

To change the download cache directory:

```sh
GHI_CACHE_DIR="$HOME/mycache" ghi get burntsushi/ripgrep
# or
ghi --cache-dir "$HOME/mycache" get burntsushi/ripgrep
```

**Important:** It is _not_ recommended to run this script in `sudo` mode to install to `/usr/local/bin` or any such location. Instead, use this script with the defaults, and copy the file manually using `sudo cp`. Why? Two reasons:

* This script doesn't protect you against untrusted tar-file or zip-file related exploits.
* `Path.home()` returns `/root` and the default cache directory changes accordingly, _and_ the downloaded files (in the cache directory) will have `root` as their owner, which will consequently require `sudo` mode to clean up.

## Alternatives

* [install-release](https://github.com/Rishang/install-release): more feature-rich Github release installer; requires installation as a python package to use
