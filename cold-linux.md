# Installing Linux on a New Laptop

## Burn the [Linux Mint XFCE](https://linuxmint.com/download.php) ISO

I prefer [XFCE](https://xfce.org) as my desktop since it's known and works well on systems with slower hardware specs.

Do make sure to [verify](https://linuxmint.com/verify.php) the ISO before burning it to ensure it is not compromised.

## Boot into Linux Mint

Leave the DVD in the DVD-ROM when restarting your computer and it should detect and boot from the Live DVD. If it does not, you can:

* Use `F2`/`Delete` to enter BIOS and change the boot order.
* Use `F12` to see the boot menu.
* Follow Windows 10 instructions for booting from a DVD.

## Install Linux Mint

Once the Live Desktop has loaded, follow these steps:

* Use Firefox to Google "diceware deb".
* Visit: https://packages.debian.org/sid/utils/diceware -> Click "all" -> Download from ftp.debian.org.
* Using the `terminal`:
  * `md5sum ~/Downloads/dice*`
  * `sha256sum ~/Downloads/dice*`
* Verify the md5 and sha256 hashes match the debian.org website.
* Using the `terminal`:
  * `sudo dpkg --install ~/Downloads/dice*.deb`

Then, **UNHOOK THE INTERNET**.

Using `diceware`, we can create ultra-secure passwords:

* On-disk encryption: `diceware -n 8 -s 6 -d ' ' -w en_eff`
* Home encryption: `diceware -n 6 -s 4 -d ' ' -w en_eff`

Long parameter names from above:

* `-n NUM --num NUM`
* `-s --special NUM`
* `-d DELIMITER --delimiter DELIMITER`
* `-w NAME --wordlist NAME`

The EFF word list was chosen for this [reason](https://www.eff.org/deeplinks/2016/07/new-wordlists-random-passphrases).

Then, start installing Ubuntu without proprietary drivers.

Preferably use a non-identifying username with a matching machine name.

## Booting Linux Mint

Type the passwords to decrypt the hard drive and login to your user, **then**: plug in the internet connection.

Use the `terminal` to run the following commands:

```
# setup gpg to use a more secure default algorithm
echo "cipher-algo AES256" >> ~/.gnupg/gpg.conf

# update the repos, then update the packages
sudo su
apt-get update && apt-get upgrade -y

# install a few useful tools
apt-get install -y tree wipe scrub bleachbit git vim terminator
```

Configure and install all software within the `Update Manager`.

Install Electrum for cold-wallets and for the online wallet to broadcast the transaction. Ensure both the cold and online wallets are using the same Electrum version.

```
# Ensure you are using the correct urls as provided by: https://electrum.org/#download

# install Electrum prereqs and allow Electrum to scan barcodes
apt-get install python3-setuptools python3-pyqt5 python3-pip zbar-tools

# update pip so it stops complaining and install wheel so Electrum doesn't complain either
pip install --upgrade pip wheel

# download Electrum and verify the tarball manually
wget https://download.electrum.org/3.0.6/Electrum-3.0.6.tar.gz
wget https://download.electrum.org/3.0.6/Electrum-3.0.6.tar.gz.asc
gpg --with-fingerprint Electrum-3.0.6.tar.gz.asc

# then install Electrum
pip3 install Electrum-3.0.6.tar.gz
```

Next, install Docker to be able to run self-contained Docker images that can be transferred to an offline computer using a DVD-ROM:

```
# use the simple Docker install script
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh

# install Docker Compose for easier Docker usage
pip3 install docker-compose

# test that the software was installed correctly
docker-compose --version
docker run -ti ubuntu:16.04

# potential security risk for networked computers
# but it allows for running docker commands without having to provide the user-password
# sudo usermod -aG docker $USER
```
