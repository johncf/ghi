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
```

To download and install the latest release:

```sh
ghi get pypa/hatch
```

To list last 30 releases:

```sh
ghi ls pypa/hatch
```

## Contributing

If you'd like to add/improve support for various platforms, please feel free to create an issue or pull request. Please note that all code must live in a single file, and adding new dependencies should be avoided. If you'd like to add a new feature, please take care to keep things simple as far as possible.

## Alternatives

* [install-release](https://github.com/Rishang/install-release): more feature-rich Github release installer; requires `pip` or `pipx` to install and use
