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

    Mac & Ubuntu:-
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
    ln -sf dotfiles/.config/zsh/.zshrc .zshrc
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

5. Resync and update the submodule:
    Navigate to dotfile directory use below commands:
    ```shell
    git submodule sync
    git submodule update
    ```
