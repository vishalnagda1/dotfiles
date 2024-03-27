# dotfiles

Dotfiles are configuration files for various programs, and they help those programs manage their functionality.


#### Why Use Dotfiles?
You spend a sufficient amount of time fine-tuning your setup. You curate configurations and settings that best suit your workflow, aesthetic, and preferences. And you end up with a development environment that helps you, personally, be more productive.

What if after all that time you spent, you now have to switch to a new, different machine? Does that mean you have to start all over again from the beginning?

No, that's where the dotfiles are coming into the picture and using dotfile all your settings and preferences can be reusable and consistent on other machine.


#### How this repo will help me?
This repo is containing the dotfiles which are related to it's author and you can use it to begain your dotfile journey by using this repo as a template.


### Getting Start
This guide section will help you to setup the dotfile configurations in your system. You have to follow commands based on your system type. If system type is not menthioned then those commands are generic and can be used in any system.

1. Install required packages
    Termux (Android):-
    ```shell
    pkg update -y
    pkg upgrade -y
    pkg install git openssh neovim starship zsh tmux -y
    chsh -s zsh
    ```

    Ubuntu:-
    ```shell
    # update, upgrade and autoclean packages
    sudo apt update -y
    sudo apt upgrade -y
    sudo apt autoremove

    # install required packages
    sudo apt install build-essential git curl wget neovim zsh tmux pass pass-extension-otp -y

    # change default shell to zsh
    chsh -s $(which zsh)

    # install oh my zsh framework and its plugins
    sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

    # install Fira Code Nerd Font
    wget https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/FiraCode.zip
    mkdir -p ~/.local/share/fonts
    unzip FiraCode.zip -d ~/.local/share/fonts
    rm ~/.local/share/fonts/README.md ~/.local/share/fonts/LICENSE FiraCode.zip
    fc-cache -fv
    echo -e "Testing Nerf Fonts: \uf00c \uf0e7 \uf304"

    # install starship
    curl -sS https://starship.rs/install.sh | sh

    # install kitty terminal
    curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
    # Add Kitty to PATH
    sudo ln -sf ~/.local/kitty.app/bin/kitty ~/.local/kitty.app/bin/kitten /usr/local/bin/
    # Create Desktop And Application Shortcuts
    cp ~/.local/kitty.app/share/applications/kitty.desktop ~/.local/share/applications/
    # If you want to open text files and images in kitty via your file manager also add the kitty-open.desktop file
    cp ~/.local/kitty.app/share/applications/kitty-open.desktop ~/.local/share/applications/
    # Update the paths to the kitty and its icon in the kitty.desktop file(s)
    sed -i "s|Icon=kitty|Icon=/home/$USER/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g" ~/.local/share/applications/kitty*.desktop
    sed -i "s|Exec=kitty|Exec=/home/$USER/.local/kitty.app/bin/kitty|g" ~/.local/share/applications/kitty*.desktop
    # Kitty config
    mkdir -p ~/.config/kitty/
    ln -sf ~/dotfiles/.config/kitty/kitty.conf ~/.config/kitty/

    sudo mkdir -p /etc/apt/keyrings
    wget -qO- https://raw.githubusercontent.com/eza-community/eza/main/deb.asc | sudo gpg --dearmor -o /etc/apt/keyrings/gierens.gpg
    echo "deb [signed-by=/etc/apt/keyrings/gierens.gpg] http://deb.gierens.de stable main" | sudo tee /etc/apt/sources.list.d/gierens.list
    sudo chmod 644 /etc/apt/keyrings/gierens.gpg /etc/apt/sources.list.d/gierens.list
    sudo apt update
    sudo apt install -y eza
    
    sudo apt install fd-find
    ln -s $(which fdfind) ~/.local/bin/fd
    sudo apt install fzf
    
    wget -qO - https://pkg.pujol.io/debian/gpgkey | gpg --dearmor | sudo tee /usr/share/keyrings/pujol.io.gpg >/dev/null
    echo 'deb [arch=amd64 signed-by=/usr/share/keyrings/pujol.io.gpg] https://pkg.pujol.io/debian/repo all main' | sudo tee /etc/apt/sources.list.d/pkg.pujol.io.list
    sudo apt-get update
    sudo apt-get install pass-extension-import
    
    LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | grep -Po '"tag_name": "v\K[^"]*')
    curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/latest/download/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
    tar xf lazygit.tar.gz lazygit
    sudo install lazygit /usr/local/bin
    lazygit --version
    
    asdf plugin add lazydocker https://github.com/comdotlinux/asdf-lazydocker.git
    asdf install lazydocker latest
    asdf global lazydocker latest
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh  # node version manager

    ```

    Mac:-
    ```shell
    # Will update soon
    ```

2. Clone the repo at your desired location
    ```shell
    git clone https://github.com/vishalnagda1/dotfiles.git --recursive
    ```

    **NOTE:** Currently we're using HTTPS to clone the repo. We will update the remote to SSH later, after setting up the ssh config.
    This repo contains the submodule called `Private`. Private (directory) is a private dotfile repo containing the personal configs like `.ssh`, `.gitconfig` etc.

    You may see cloning failed info because the gitsubmodule is using ssh based url.

3. Goto the dotfile repo and update the submodule
    ```shell
    cd dotfiles
    ```

    Update the private repo URL in .gitmodules (use HTTPS url for now later we will update it to SSH)
    
    ```shell
    vi .gitmodules
    ```
    **NOTE:** I'm using `vi` editor, you can use any of your choice.
    
    **NOTE:** Also note that you've to create git [token](https://github.com/settings/tokens) in order to use private repo with HTTPS and when it asks for username and password. Use your git username and token as the password.

    Update the submodule:

    ```shell
    git submodule sync
    git submodule update
    ```

    Now navigte to your private repo:
    ```shell
    cd Private
    git checkout main
    git remote set-url origin <your private repo ssh url>
    ```

    Naviagte to dotfiles directory & update the remote url from HTTPS to SSH:
    ```shell
    cd ..
    git remote set-url origin <your dotfiles repo ssh url>
    ```

4. Symlink your dotfiles:
    **NOTE:** My dotfiles path is user's home directory i.e. `~/dotfiles`
    **NOTE:** I am removing the existing .ssh directory.
    ```shell
    cd
    rm -rf .ssh
    ln -sf dotfiles/.ssh .ssh
    ln -sf dotfiles/.config/git/.gitconfig .gitconfig
    ```

    If you're using zsh shell use below command:
    ```shell
    ln -sf dotfiles/.config/zsh/.zshrc .zshrc
    ```

    If you're using bash shell use below command:
    ```shell
    ln -sf dotfiles/.config/bash/.bashrc .bashrc
    ```

    Linking config of nvim:
    ```shell
    mkdir -p ~/.config/nvim/
    cd ~/.config/nvim/
    ln -sf ~/dotfiles/.config/nvim/init.vim init.vim
    ```

    Termux:
    ```shell
    rm -rf .termux
    ln -sf dotfiles/.config/termux/ .termux
    ```

    You may need to update nerd fonts in termux:
    ```shell
    curl -O https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/FiraCode/Regular/FiraCodeNerdFont-Regular.ttf
    mv FiraCodeNerdFont-Regular.ttf .termux/font.ttf
    ```

5. Update ssh key permission and add ssh key to the agent:
    ```shell
    cd
    chmod 400 ~/.ssh/id_ed25519
    chown $USER ~/.ssh/config
    chmod 644 ~/.ssh/config
    ssh-add
    ```

    To verify the added ssh key:
    ```shell
    ssh-add -l
    ```

6. Resync and update the submodule:
    Navigate to dotfile directory use below commands:
    ```shell
    git checkout .
    git submodule sync
    git submodule update
    ```

7. Install additional GIU softwares (Optional):
    Ubuntu:
    ```shell
    sudo snap install --classic code
    sudo snap install postman
    ```

8. Install Docker CLI
   Ubuntu:
   Run the following command to uninstall all conflicting packages:
   ```shell
   for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
   ```

   Set up Docker's apt repository:
   ```shell
   # Add Docker's official GPG key:
   sudo apt-get update
   sudo apt-get install ca-certificates curl
   sudo install -m 0755 -d /etc/apt/keyrings
   sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
   sudo chmod a+r /etc/apt/keyrings/docker.asc
   
   # Add the repository to Apt sources:
   echo \
     "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
     $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
     sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   ```

   To install the latest version, run:
   ```shell
   sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
   ```

   Start docker service:
   ```shell
   sudo service docker start
   ```

9. OPTIONAL - Setting up Ollama (Local AI Chat)
   Ubuntu
   ```shell
   curl -fsSL https://ollama.com/install.sh | sh
   ```

