# rsync-paste.yazi

**Just a simple plugin to copy/paste in [Yazi](https://github.com/sxyazi/yazi) using rsync.**


## Instructions:

1. Press `y`
2. Go to destination
3. Press `SHIFT + P`


## Warning

Existing files may be overwritten if they differ from the source.


## Requirements

- Yazi 26.9.1 (tested)
- rsync installed
- Void Linux (tested)


## Installation

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


## AI Assistance

I used OpenAI's ChatGPT (GPT-6).

ChatGPT assisted with the Lua implementation, debugging, and documentation. The plugin's concept, functionality, design decisions, and testing were made by me.

The project is maintained by me. No copyright ownership or authorship is claimed on behalf of ChatGPT or OpenAI.


## License

MIT License. See [LICENSE](LICENSE).
