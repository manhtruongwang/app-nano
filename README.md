# blue-app-nano

$NANO wallet application for Ledger Nano S & Ledger Blue devices.

## For users

You can install the Nano app from the Ledger Manager. If it doesn't show up for you in Ledger Manager, make sure that your Ledger device firmware has been upgraded to the latest version. See also the Ledger own [guide on installing and using the app](https://support.ledgerwallet.com/hc/en-us/articles/360005459013-Install-and-use-Nano).

To interact with the Nano network, you need to use a wallet software that has integrated Ledger support. Currently the following wallets have integrated Ledger support:

- [Nault.cc](https://nault.cc/) ([user guide](https://docs.nault.cc/2020/08/04/ledger-guide.html))

_If a wallet is missing from above, please [create an issue](https://github.com/roosmaa/blue-app-nano/issues/new) and it will be added to this list._

## For wallet developers

If you wish to integrate your $NANO web wallet with Ledger, then you can use the [hw-app-nano](https://github.com/roosmaa/hw-app-nano/) JavaScript library that works in tandem with [ledgerjs](https://github.com/LedgerHQ/ledgerjs) library.

For desktop wallet apps, there is no integration library at the time. But you can still interact with the device using the binary protocol detailed in [the ADPU documentation](https://github.com/roosmaa/blue-app-nano/blob/master/doc/nano.md).

Ledger Signing Fix After FW Updates

Remember, this is an temporary fix, this will skip the block confirmation screen and sign whatever is sent to the Ledger so double check your input. I will not take responsibily for any problem that this modifications may caused.

Prepare:
- Ubuntu VM with USB Passthrough (Mac with Parallels,...) or an Ubuntu Host
- Ledger Device (S, S+, X,...)

Step 1 - Install Docker

# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update

# Install Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Step 2 - Install the app
git clone https://github.com/manhtruongwang/app-nano
cd app-nano

# Plug your Ledger to PC, enter PIN and stay on app select screen
sudo docker run --rm -ti  -v "$(realpath .):/app" --privileged -v "/dev/bus/usb:/dev/bus/usb" ghcr.io/ledgerhq/ledger-app-builder/ledger-app-builder:latest

# Install it to Ledger and with accept prompt on Ledger

For Banano on Ledger S: COIN=banano BOLOS_SDK=$NANOS_SDK make load
For Nano on Ledger S: COIN=nano BOLOS_SDK=$NANOS_SDK make load

For Banano on Ledger S+: COIN=banano BOLOS_SDK=$NANOSP_SDK make load
For Nano on Ledger S+: COIN=nano BOLOS_SDK=$NANOSP_SDK make load

For Banano on Ledger X: COIN=banano BOLOS_SDK=$NANOX_SDK make load
For Nano on Ledger X: COIN=nano BOLOS_SDK=$NANOX_SDK make load

You can now use Ledger device with Nault for Nano/TheBananoStand for Banano

