# Post-Arch Install Guide

> Author: David Boyd<br>
> Date: 2023-03-20

|                        |            |
|------------------------|------------|
| OS                     | Arch Linux |
| DE                     | KDE Plasma |
| Communication Protocol | X11        |

## 1. Dependencies

``` bash
###
### Make life easier
###
# 1. Alias to skip 'sudo' for a few programs
echo "alias pacman='sudo pacman'" >> ~/.bashrc
echo "alias systemctl='sudo systemctl'" >> ~/.bashrc

###
### Terminal Programs
###
# 1. Install Yay AUR Helper
pacman -S --needed git base-devel
pacman -S fakeroot
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si

# 2. Install various shell programs
pacman -S bat cups fzf cpanminus xclip neovim tmux zsh npm ruby python3 python-pip mlocate firefox qutebrowser virt-manager vivaldi --noconfirm
yay -S ungoogled-chromium-bin librewolf

### Installing ZSH Guide: https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH
# 3. Verify zsh installation
zsh --version 
# Set ZSH as your default shell
chsh -s $(which zsh)
# Reboot
reboot
# Verify default shell is ZSH
echo $SHELL

### Installing OMZ Guide: https://github.com/ohmyzsh/ohmyzsh
# 1. Install OMZ
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# 2. Re-open terminal
exit
# 3. Install Plugins: Autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# 4. Install Plugins: Syntax-Highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
# 5. Install Autojump
git clone https://github.com/wting/autojump.git
./autojump/install.py

### LogiOps Install Guide: https://github.com/PixlOne/logiops
# 1. Install dependencies
pacman -S cmake libevdev libconfig pkgconf
# 2. Clone and build
git clone https://github.com/PixlOne/logiops.git
mkdir build && cd build && cmake .. && make
# 3. Install then enable service
sudo make install
systemctl enable --now logid

### Keyd Install Guide: https://github.com/rvaiya/keyd
git clone https://github.com/rvaiya/keyd
cd keyd && make && sudo make install
systemctl enable --now keyd
```

## 2. Personalizing

``` bash
# Install various fonts
pacman -S ttf-meslo-nerd otf-cascadia-code-nerd otf-firamono-nerd \
  ttf-liberation noto-fonts powerline-fonts noto-fonts-cjk
yay -S gsfonts

# Powerlevel10K Install Guide: https://github.com/romkatv/powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
# (Optional) Update the .zshrc ZSH_THEME accordingly
ZSH_THEME="powerlevel10k/powerlevel10k"
```

## X. Printers

1. Install cups
2. `systemctl enable --now cups`
3. Install GUI program: 
    - `pacman -S system-config-printer` # Auto-detect printer
    - KDE Plasma: `pacman -S print-manager` # KDE GUI for printers
4. Install printer driver: https://wiki.archlinux.org/title/CUPS/Printer-specific_problems
    - `yay -S brlaser`   # Bother Laser Printers
    - `pacman -S hplip`  # HP Printers
5. Setup Avahi (Network Discovery): https://wiki.archlinux.org/title/Avahi#Hostname_resolution
    - `pacman -S nss-mdns`
    - Install, enable, and start Avahi: 
      `pacman -S avahi && systemctl enable --now avahi-daemon.service`
    - Edit and change the `hosts` line in the `/etc/nsswitch.conf` file:
    	- `hosts: mymachines mdns_minimal [NOTFOUND=return] resolve [!UNAVAIL=return] files myhostname dns`
6. Install printer (via KDE GUI Settings > Printers):
    1. Click `Add Printer`
    2. Click `Manual URI` ***AND/OR*** wait for printer box to populate
    3. Click **Discovered Network Printers** > `Brother DCP-L2540DW series` 
    4. Choose **Connections** > `IPP network printer via DNS-SD`
    5. Choose previously installed driver: `Brother DCP-L2540DW series, using brlaser v6 (en)`
    6. Continue through remaining self-guided options and test print.

7. Set up Line Print Options:
    1. Check the term's default printer setup: `lpstat -d`
    2. If none appear, list all available printers: `lpstat -p`
    3. Set term's default printer: `lpoptions -d <printerName>`

?. Start cups-browsed service (Network printers) ## Doesn't seem necessary

NOTE: May need to restart the Avahi service.

## 3. NeoVim-ing Providers

``` bash
### Python / PIP
# 1. Enable the Python3 Provider
pip3 install --user --upgrade pynvim  # (Note: 'neovim' is deprecated)
# 2. Install NeoVim-Remote (nvr)
pip3 install --user --upgrade neovim-remote
# 3. TEST
nvim -c "py3 print('hello')"

### Ruby
# 1. Add to PATH 
export PATH="$PATH:$(ruby -e 'puts Gem.user_dir')/bin' \
&& gem list && gem update 
# 2. Install Ruby's NeoVim module
gem install neovim
# (Optional) Get PATH of Ruby
gem environment

### NodeJS
sudo npm install -g neovim

### Perl
sudo cpanm -n Neovim::Ext
```

## 4. Neovim Dotfiles

### CheckHealth Pass

1. Install dependencies.  Use `:checkhealth` to verify installs & integration:
- `pacman -S fd`
2. Resolve Perl provider write access: 
`cpanm --local-lib=~/perl5 local::lib && eval $(perl -I ~/perl5/lib/perl5/ -Mlocal::lib)`

#### Notes 

- Python & Ruby's `vim.g.{}_host_prog` are set in the `init.lua`
- TMUX issues are resolved in the `$HOME/.tmux.conf` file.

### Packer - Plugin Manager

1. When using Arch, install via AUR: `yay -S nvim-packer-git`
2. Setup plugins: `~/.config/nvim/lua/plugins.lua`
3. Compile, Install, Sync Packer: `vim +PackerCompile`, `:PackerInstall`,
   `:PackerSync`

### COC (Code of Completion)

**REF:** https://github.com/neoclide/coc.nvim/wiki/Using-coc-extensions

1. `CocInstall <extensionNames>`

## ?. Other Notes

OBS Flickering: System Settings > Display & Monitor > Compositor >
[Uncheck] Allow applications to block compositing

