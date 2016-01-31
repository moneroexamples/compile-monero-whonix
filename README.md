# Compile Monero 0.9 on Whonix-Workstation for VirtualBox
[Monero](https://getmonero.org/) and [Whonix](https://www.whonix.org/) are tools
that privacy centric users can use as part of their privacy enhancing toolbox.

One problem with Monero is that, if you want to run full Monero node, your
IP address will be exposed to others in the Monero network. This, for some,
might be not very good idea.

One way to overcome this problem is to run the node through Tor. And this can be done having the Monero node running inside the Whonix.

## Preparation
 Assuming that you have Whonix setup into your VirtualBox, the first thing that
 should be done is to increase Whonix-Workstation's ram. The default size
 is 768 MB, and this is not enough for compilation. I usually set it up to 2 GB, but I think 1GB should also be good.

 ```bash
 VBoxManage modifyvm Whonix-Workstation --memory 2048
 ```

## Compilation
Start your Whonix-Workstation and do the following in the workstation.

```bash
# install dependencies
sudo apt-get install build-essential cmake libboost1.55-all-dev miniupnpc  libunbound-dev graphviz doxygen liblmdb-dev libssl-dev pkg-config

# download the latest bitmonero source code from github
git clone https://github.com/monero-project/bitmonero.git

# go into bitmonero folder
cd bitmonero/

# compile
make release-static-32
```

After successful compilation, the Monero binaries should be located in `./bin`

I usually move the binaries into `/opt/bitmonero/` folder, so this can be done
as follows:
```
sudo mkdir /opt/bitmonero
sudo mv -v ./build/release/bin/* /opt/bitmonero/
```

To start now the only think left is to start the Monero daemon and let it
download the blockchain and synchronize with the Monero network. After that,
you can run your the `simplewallet`.

Please note that downloading the full blockchain will probably be very slow. So it would be better to download it independently
and then copy to the default Monero folder, i.e., `~/.bitmonero/lmdb/`

```bash
# launch the Monero node daemon and let it synchronize with the Monero network
/opt/bitmonero/bitmonerod

# launch the Monero wallet
#/opt/bitmonero/simplewallet
```

## Example screenshot

**Commands used to start the nodes and wallets:**
![Before](https://raw.githubusercontent.com/moneroexamples/compile-monero-whonix/master/img/whonix_monero.jpg)

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.

Some Monero are also welcome:
```
48daf1rG3hE1Txapcsxh6WXNe9MLNKtu7W7tKTivtSoVLHErYzvdcpea2nSTgGkz66RFP4GKVAsTV14v6G3oddBTHfxP6tU
```    
