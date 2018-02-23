# Install an Online Linux Computer

This is a continuation for the steps to install an [offline laptop](/cold-linux), so some steps may be repeated.

## Update the Machine and Install Some Useful Software

```
echo "cipher-algo AES256" >> ~/.gnupg/gpg.conf

sudo su
apt-get update && apt-get upgrade -y
apt-get install -y terminator firejail ufw clamtk git gparted htop youtube-dl vim vlc curl cheese tree wipe scrub bleachbit fail2ban redshift
```

## Install the Best [Private Internet Access](https://privateinternetaccess.com) Support

```
wget https://www.privateinternetaccess.com/installer/pia-nm.sh
sudo bash pia-nm.sh
```

## Use the GUI

* Configure `Software Updater`.
* Use the `Welcome Screen` to:
  * Install `Media Codecs`.
  * Install `Device Drivers`.
* `Application Manager` to install: `Chromium`, `Sublime`.
* Configure `Terminator`: Preferences -> Profiles -> Copy on selection

## Install Tor

Visit https://www.torproject.org/download/download-easy.html.en, then:

```
gpg --with-fingerprint tor*.asc
mkdir -p ~/Applications
mv tor* ~/Applications
cd ~/Applications
tar xf tor*.tar.gz
cd tor*
./start-tor-browser.desktop
```

## Internet Browsers

Setup three different browsers shortcuts:

* `firejail firefox %u`
* Start Chrome once, then: `firejail chromium-browser %U`
* `firejail --private firefox -no-remote https://start.duckduckgo.com`
* `~/Applications/tor*/start-tor-browser.desktop`

### Setup Extensions for the 1st Firefox Shortcut and Chrome

* HTTPS Everythwere
* Disconnect
* uBlock Origin
* LastPass

Configure Chrome: Settings -> Manage passwords -> Off

## Install Docker

```
curl -fsSL get.docker.com -o get-docker.sh
sh get-docker.sh
pip3 install docker-compose

# verify it works
docker-compose --version
docker run -ti ubuntu:16.04
```

## Configure the Datetime Toolbar Indicator

* Layout, Format: Date only
* Date, Format, Custom: %a %b %d %l:%M:%S %p
* Time, Format, Custom: <blank> 

## Install PyCharm

Visit: https://www.jetbrains.com/pycharm.

Exract the tarball into `~/Applications/`.
