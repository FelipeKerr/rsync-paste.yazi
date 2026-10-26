# rsync-paste.yazi

**Incremental local copy/paste for [Yazi](https://github.com/sxyazi/yazi) using rsync.**

Copy files and directories using Yazi's native yank workflow, while letting `rsync` skip unchanged files and display transfer progress directly in Yazi's header.

No destination paths to type, no confirmation dialogs, and no unnecessary file transfers.

## Features

- **Native workflow:** Yank files with `y`, navigate to the destination, and press `Shift+P`.
- **Incremental copying:** Uses `rsync` to skip unchanged files.
- **Live progress:** Displays transfer progress in Yazi's header.
- **Local transfers:** Copies between local directories, including mounted drives.
- **No deletions:** Files that exist only in the destination are preserved.
- **No confirmation dialogs:** Transfers start immediately.
- **Non-destructive integration:** Yazi's native paste (`p`) and cut (`x`) commands remain unchanged.

## Requirements

- Yazi with the plugin APIs used by this plugin (tested on Yazi 26.9.1)
- `rsync` installed and available in your `PATH`
- Linux (currently tested on Void Linux)

Other Unix-like systems may work but have not been tested.

## Installation

Install the plugin using Yazi's package manager:

```sh
ya pkg add FelipeKerr/rsync-paste
```

Alternatively, clone the repository manually:

```sh
git clone https://github.com/FelipeKerr/rsync-paste.yazi.git \
  ~/.config/yazi/plugins/rsync-paste.yazi
```

Add the following keybinding to your `~/.config/yazi/keymap.toml`:

```toml
[[mgr.prepend_keymap]]
on   = "P"
run  = "plugin rsync-paste"
desc = "Incremental paste using rsync"
```

No additional configuration is required.

## Usage

1. Select one or more files or directories in Yazi.
2. Press `y` to yank them.
3. Navigate to the destination directory.
4. Press `Shift+P` to start copying.

The transfer starts immediately. Progress is displayed in Yazi's header, and a notification appears when the operation finishes.

You can continue using Yazi while the transfer runs.

### How it works

The plugin runs `rsync` with these options:

```sh
rsync -ah --info=progress2 --outbuf=L -- SOURCE... DESTINATION/
```

- `-a`: Archive mode; recursively copies directories and preserves supported file attributes.
- `-h`: Human-readable output.
- `--info=progress2`: Reports overall transfer progress.
- `--outbuf=L`: Uses line-buffered output.

By default, `rsync` compares file size and modification time to decide whether a file needs to be transferred.

Existing destination files may be updated or overwritten if they differ from the source. Files that exist only in the destination are not deleted.

The plugin does not use `--delete` or `--checksum`.

## Limitations

- **Local copying only:** Remote destinations over SSH are not supported through the plugin interface.
- **Copy only:** Yanked files marked for cutting/moving (`x`) are rejected.
- **No conflict dialog:** Existing files may be overwritten according to `rsync`'s normal behavior.
- **No cancellation interface:** The plugin does not currently provide a dedicated transfer cancellation command.
- **Symbolic links:** Source/destination safety checks use path comparisons and do not fully resolve symbolic links.

## License

MIT License. See [LICENSE](LICENSE).
