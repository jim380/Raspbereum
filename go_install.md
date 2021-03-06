# Install Go
[ [Intro](README.md) ] -- [ [Set Up RasPi](pi_setup.md) ] -- [ **Install Go** ] -- [ [Install Geth](geth_install.md) ] -- [ [Run Geth](geth_run.md) ] -- [ [FAQ](faq.md) ] -- [ [Updates](raspi_updates.md) ]

-----
## Preparation
- `$ sudo apt-get update`
- `$ sudo apt-get upgrade -y`
- `$ sudo apt-get install htop git curl bash-completion jq`
- `$ sudo apt-get install libgmp3-dev -y`
## Install Golang
Run this [bash](https://github.com/jim380/node_tooling/blob/master/Cosmos/CLI/go_install.sh) script if you feel lazy. Otherwise, proceed. 
- Download the archive<br/>`$ wget https://dl.google.com/go/go1.11.linux-armv6l.tar.gz`
<br/>![download](pics/go_install/download.jpg)

- Extract it into /usr/local, creating a Go tree in /usr/local/go<br/>`$ sudo tar -C /usr/local -xvf go1.11.linux-armv6l.tar.gz`
<br/>![tar](pics/go_install/tar.jpg)

- Change owner to root, and change permissions<br/>`$ sudo chown root:root /usr/local/go`<br/>`$ sudo chmod 755 /usr/local/go`
<br/>![permission](pics/go_install/permission.png)

- Create a workspace folder, and 3 sub-folders inside it<br/>`$ mkdir <workspace_name>{,/bin,/pkg,/src}`<br/>*name it whatever you want, here I just named it `workspace`*
<br/>![workspace](pics/go_install/workspace.jpg)

- Set environment variables
<br/>~ open up the file: `$ sudo nano /etc/profile`
<br/>~ add this line to at the end of the file: `export PATH=$PATH:/usr/local/go/bin`
<br/>![path_1](pics/go_install/path_1.jpg)
<br/>`$ cd`
<br/>~ open up the file:`$ sudo nano .profile`
<br/>~ add the following lines at the end of the file:
<br/>`export GOPATH=$HOME/<workspace_name>`
<br/>`export PATH=$HOME/<workspace_name>/bin:$PATH`
<br/>![path_2](pics/go_install/path_2.jpg)
  
- Reboot<br/>`$ sudo shutdown -r now` 
## Test if Go is correctly installed and working
- `$ go version`
- `$ go env`
<br/>![check_installation](pics/go_install/check_installation.jpg)

## Unstall Golang
- `$ sudo apt remove golang`
- `$ sudo apt-get autoremove`
- `$ source .profile`

-----

Next: [Install Geth >>](geth_install.md)
