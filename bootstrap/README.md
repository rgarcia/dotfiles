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
