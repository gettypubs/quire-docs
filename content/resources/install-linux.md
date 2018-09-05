---
title: Quire Installation
subtitle: LINUX
type: page
---

### LINUX Users:

1. Open terminal (If you are coming from the Windows 10 instructions this should already be open)

2. Download and install **Prince**:
   
   ```
   cd ~
   ```

   Run these commands to download and install PrinceXML 

   ```sh
   wget https://www.princexml.com/download/prince_12-1_ubuntu18.04_amd64.deb

   sudo gdebi prince_10r2-1_debian8.0_amd64.deb
   ```
   
   If you chose a different distribution of Linux there are more instructions here -> https://www.princexml.com/doc-install/#linux
   
3. Install **node js and npm through nvm**

   Detailed information here -> https://github.com/creationix/nvm#install-script

   To install or update nvm, you can use the [install script][2] using cURL:

    ```sh
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
    ```

    or Wget:

    ```sh
    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
    ```

    <sub>The script clones the nvm repository to `~/.nvm` and adds the source line to your profile (`~/.bash_profile`, `~/.zshrc`,      `~/.profile`, or `~/.bashrc`).</sub>

    ```sh
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    ```

    **Note:** You can add `--no-use` to the end of the above script (...`nvm.sh --no-use`) to postpone using `nvm` until you manually [`use`](#usage) it.

    You can customize the install source, directory, profile, and version using the `NVM_SOURCE`, `NVM_DIR`, `PROFILE`, and `NODE_VERSION` variables.
    Eg: `curl ... | NVM_DIR="path/to/nvm"`. Ensure that the `NVM_DIR` does not contain a trailing slash.

    <sub>*NB. The installer can use `git`, `curl`, or `wget` to download `nvm`, whatever is available.*</sub>

    **Note:** On Linux, after running the install script, if you get `nvm: command not found` or see no feedback from your terminal after you type:

    ```sh
    command -v nvm
    ```
    simply close your current terminal, open a new terminal, and try verifying again.


    If the above doesn't fix the problem, open your `.bash_profile` and add the following line of code:

    `source ~/.bashrc`

    - For more information about this issue and possible workarounds, please [refer here](https://github.com/creationix/nvm/issues/576)

    ### Verify installation

    To verify that nvm has been installed, do:

    ```sh
    command -v nvm
    ```

    which should output 'nvm' if the installation was successful. Please note that `which nvm` will not work, since `nvm` is a sourced shell function, not an executable binary.

    To download, compile, and install the latest release of node, do this:

    ```sh
    nvm install node
    ```

    And then in any new shell just use the installed version:

    ```sh
    nvm use node
    ```
4. Install **Pandoc** for EPUB and MOBI output 

   ```
   cd ~
   ```

   Visit https://github.com/jgm/pandoc/releases and download the latest .deb file

   ```
   wget https://github.com/jgm/pandoc/releases/download/2.2.3.2/pandoc-2.2.3.2-1-amd64.deb
   ```
   Install the .deb file
   
   ```
   sudo dpkg -i pandoc-2.2.3.2-1-amd64.deb
   ```

   This will install the pandoc and pandoc-citeproc executables and man pages.

   Verify pandoc was installed

   ```
   pandoc -v
   ```

   If Pandoc version information is returned then Pandoc was successfully installed on your system.

5. Install **Quire-CLI**

    ```
    git clone https://github.com/gettypubs/quire-cli
    ```
    
    ```
    cd quire-cli
    ```
    
    ```
    git checkout pc-dev
    ```
    
    Install Dependencies
    
    ```
    npm install -g
    ```
    
    Verify
    
    ```
    quire -V
    ```
    
    If version number is returned quire-cli was installed correctly, you can now leave the directory.

    ```
    cd ~
    ```

6. Start a new **Quire** project

    Create a new project

    ```
    quire new your-project-name
    ```
    Enter the new directory

    ```
    cd your-project-name
    ```

    Install starter theme dependencies

    ```
    quire install
    ```
    
    then to start editing run
    
    ```
    quire preview
    ```

    Once running, open a browser and visit [http://localhost:1313](http://localhost:1313) to see the publication.

