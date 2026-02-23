# Bootstrap a New Mac

This folder is a quick-reference checklist for setting up a fresh machine.

## 1) Bring the Brewfile

Copy your existing `Brewfile` to the new computer (for example via SSH or a USB drive).

- This repo includes a copy at `bootstrap/Brewfile`.
- Place it wherever you want to run `brew bundle` from.

## 2) Install Homebrew

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Run the final setup instructions shown by the installer. If needed for zsh on Apple Silicon:

```sh
echo >> "$HOME/.zprofile"
echo 'eval "$(/opt/homebrew/bin/brew shellenv zsh)"' >> "$HOME/.zprofile"
eval "$(/opt/homebrew/bin/brew shellenv zsh)"
```

## 3) Install Oh My Zsh

```sh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## 4) Install packages from Brewfile

Open a new terminal, then run:

```sh
brew bundle --file=./Brewfile
```

## 5) Launch apps that need manual setup

- `1Password`: sign in, then enable CLI integration in Developer settings.
- `Raycast`: sign in, disable Spotlight shortcut, and switch Raycast to `Cmd+Space`.
- `Chrome`: sign in to Google account(s), set up profiles, add 1Password extension if needed.
- `ngrok`: sign in via browser and run the macOS setup command from <https://dashboard.ngrok.com/get-started/setup/macos>.
- `Tailscale`: sign in and set it to launch at login.
- `gh`: run `gh auth login` and configure an SSH key.

### Raycast shortcut notes

1. Open **System Settings > Keyboard > Keyboard Shortcuts > Spotlight**.
2. Uncheck **Show Spotlight search**.
3. Configure Raycast to use `Cmd+Space`.

## 6) Set up chezmoi

```sh
chezmoi init git@github.com:rgarcia/dotfiles
```

Look up the `OP_*` token in the "sa" vault, then initialize with:

```sh
OP_SERVICE_ACCOUNT_TOKEN=... chezmoi init
```

## 7) Install Doom Emacs

```sh
git clone --depth 1 https://github.com/doomemacs/doomemacs ~/.config/emacs
~/.config/emacs/bin/doom install
```

## 8) Install Claude Code

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

Then log in with:

```sh
claude
```

## 9) Install Cursor CLI

```sh
curl https://cursor.com/install -fsS | bash
```

Then log in with:

```sh
agent
```

## 10) (Optional) Copy MCP config from an existing computer via `agent`

Once `agent` is available on the new machine, you can ask it to migrate MCP config from your old machine over SSH.

1. Open a terminal on the new machine and run:

```sh
agent
```

2. Paste a prompt like this (replace placeholders):

```text
SSH to <old-user>@<old-host> and:
- copy remote ~/.cursor/mcp.json to local ~/.cursor/mcp.json (wholesale)
- copy remote ~/.claude.json to a temp file
- merge only the top-level mcpServers key from remote ~/.claude.json into local ~/.claude.json
- find Berkeley Mono fonts on the old Mac (look for TX-02-* files in ~/Library/Fonts and /Library/Fonts)
- copy any TX-02-* font files to local ~/Library/Fonts
- verify the copied font files exist locally
- validate both local JSON files are still valid
- clean up any temp files
```

3. Review the result and restart tools if needed (Cursor/Claude) so new MCP server settings are picked up.
