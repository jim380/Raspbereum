# Run Geth
[ [Intro](README.md) ] -- [ [Set Up RasPi](pi_setup.md) ] -- [ [Install Go](go_install.md) ] -- [ [Install Geth](geth_install.md) ] -- [ **Run Geth** ]   -- [ [FAQ](faq.md) ] -- [ [Updates](raspi_updates.md) ]

-----
## Create a new account
**The account consists of an encrypted private key and the corresponding public key/address, all of which are stored in `~/.ethereum` by default**
- Create a new account
<br/>`geth --datadir /mnt/hdd/eth_data account new`
<br/>Enter a passphrase twice for your new account when asked. **Make sure to remember this passphrase!!!**
<br/>![3](pics/geth_run/3.jpg)
## Start syncing with the blockchain
- "fast sync" algorithm which syncs pruned blockchain data<br/>`geth --datadir /mnt/hdd/eth_data --syncmode=fast --cache=1024`

After running this command, you should see messages as shown in the pic below.
<br/>![4](pics/geth_run/4.jpg)
<br/>After some initial synchronisation process, you should see a command line interface where you can interact with. For example:
- To check synchronisation status<br/> `eth.syncing`
This will give you current block number, and the highest block number being reported by your peers.

- To stop geth console<br/> `exit`
## Run Geth in the backgrouod (optional)
- `geth --verbosity 0 &`

### Find all Geth commands [here](https://github.com/ethereum/go-ethereum/wiki/Command-Line-Options)

**Block synchronisation takes a few days so please be patient. Also expect hiccups while the node is catching up with the blocks. Imports might occasionally stop. Sometimes you might even run into runtime errors. During these times you will need to stop and restart the node.**

**In case where the blockchain database got corrupted, you would have to rebuild the block index. To do this, delete the blockchain data and start over. To avoid such headaches, I recommend downloading the whole blockchain onto a hard drive on a computer first, then copy the `chaindata` folder over onto the Pi.**

**If you have any questions, please reach out to me on Twitter @jim380, or on Telegram @jim380. Thank you very much for checking out.**

-----
Next: [FAQ >>](faq.md)
