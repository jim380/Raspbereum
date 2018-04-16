# Run Geth
[ [Intro](README.md) ] -- [ [Set Up RasPi](pi_setup.md) ] -- [ [Install Go](go_install.md) ] -- [ [Install Geth](geth_install.md) ] -- [ **Run Geth** ]   -- [ [Updates](raspi_updates.md) ]

-----
## Create a new account
**The account consists of an encrypted private key and the corresponding public key/address, <br/>all of which are stored in `~/.ethereum` by default**
- `sudo su`
- `geth account new`
Enter a passphrase twice for your new account when asked. **Make sure to remember this passphrase!!!**
<br/>![3](pics/geth_run/3.jpg)
