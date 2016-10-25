# New Mac Setup

## Shell

Make sure you are using bash

- Finder -> Applications -> System Preferences -> Users & Groups
- right click on the user you wish to change and select **Advanced Options**
- change **Login Shell** to `/bin/bash`

## Bash Profile

```bash
touch /.bash_profile
```

And put some stuff in there.

## Programs
**Install in order**

1. [XCode](https://developer.apple.com/download/)
1. [XCode command line tools](https://developer.apple.com/download/more/)
1. [homebrew](http://brew.sh)

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```
    
2. [git](https://github.com)

    ```bash
    brew install git
    ```
    
    #### Add name and email address:

    ```bash
    git config --global user.name 'Your Name'
    git config --global user.email 'your_email@domain.com'
    ```

    #### SSH Keys
    
    ##### Create keys
  
    ```bash
    ssh-keygen -t rsa -b 4096 -C "your_email@domain.com"
    ``` 
    
    ##### Add to ssh-agent
    ```bash
    eval "$(ssh-agent -s)"
    ssh-add ~/.ssh/id_rsa
    ```
    
    ##### Add to account
    - Copy key to clipboard
    
        ```bash
        pbcopy < ~/.ssh/id_rsa.pub
        ```
        
    - In the top right corner of any page, click your profile photo, then click **Settings**.
    - In the user settings sidebar, click **SSH and GPG keys**.
    - Click **NEW SSH key or Add SSH key**
    - In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".
    - Paste your key into the "Key" field.
    - Click **Add SSH key**.
    - If prompted, confirm your GitHub password.

    #### Create global gitignore

    This is usefull if you don't want to add the same file to `.gitignore` in every repo. Like `.DS_Store`.

    ```bash
    git config --global core.excludesfile '~/.gitignore_global'
    ```
    
    Now put some sutff in there you want to globally ignore (like .DS_Store)
    
    ```bash
    echo .DS_Store > ~/.gitignore_global
    ```

1. Google Chrome
    ```bash
    brew install google-chrome
    ```

1. Java JDK
    ```bash
    brew install java
    ```

1. AWS CLI
    ```bash
    brew intsall awscli
    ```

1. Sublime
    ```bash
    brew cask install sublime-text
    ```
    
    Create `subl` symlink
    ```bash
    ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/su
    ```
    
1. Python
    ```bash
    brew install python
    pip install --upgrade pip setuptools
    ```

1. R/RStudio

    #### Preperations:
    ```bash
    brew install gcc
    brew install postgresql # for connecting to postgresql databases
    ```
          
    #### R
    ```bash
    brew tap homebrew/science
    brew install R
    ```
          
    Take care of some `brew doctor` warnings per [this](http://apple.stackexchange.com/questions/125853/homebrew-doctor-warnings-requesting-library-deletions/143143):
    
    ```bash
    brew tap homebrew/dupes
    brew install tcl-tk --with-tk
    
    mv /usr/local/lib/libtcl8.6.dylib /usr/local/lib/libtcl8.6.dylib.bak
    mv /usr/local/lib/libtk8.6.dylib /usr/local/lib/libtk8.6.dylib.bak
    ```
    
    Then link the files, so that R can find the tcl/tk install by Homebrew:
    ```bash
    ln -s /usr/local/Cellar/tcl-tk/8.6.1/lib/libtcl8.6.dylib /usr/local/lib/libtcl8.6.dylib
    ln -s /usr/local/Cellar/tcl-tk/8.6.1/lib/libtk8.6.dylib /usr/local/lib/libtk8.6.dylib
    ```
          
    #### RStudio
    
    ##### Stable
    
    ```bash
    brew cask install rstudio
    ```
        
    ##### Preview Release
    
    ```bash
    brew tap caskroom/versions
    brew cask install rstudio-preview
    ```
        
    To update RStudio Preview to a new release:
    
    ```bash
    brew cask install --force rstudio-preview
    ```
        
    #### Caveats
    
    ##### rJava
    RStudio wont work with rJava out of the box, so we must first create a symlink to dylib that RStudio can't find.
        
    ```bash
    ln -s $(/usr/libexec/java_home)/jre/lib/server/libjvm.dylib /usr/local/lib
    ```
    
    ##### Proxy
    
    ```bash
    echo http_proxy=http://proxy.net:port > ~/.Renviron
    echo https_proxy=http://proxy.net:port >> ~/.Renviron
    ```
1. LaTeX
```bash
brew install mactex
```
