# Ledger hot-fix for Nano/Banano app after firmware update (1.4.0 - S+)

#### Remember, this is an temporary fix, this will skip the block confirmation screen and sign whatever is sent to the Ledger so double check your input. I will not take responsibily for any problem that this modifications may caused.

## Prepare:

- Ubuntu VM with USB Passthrough (Mac with Parallels,...) or an Ubuntu Host
- Ledger Device (S, S+, X,...)

## Step 1 - Install Docker

### Add Docker's official GPG key:

```
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

### Add the repository to Apt sources:

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

### Install Docker

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

## Step 2 - Install the app

```
git clone https://github.com/manhtruongwang/app-nano
cd app-nano
```

### Plug your Ledger to PC, enter PIN and stay on app select screen

```
sudo docker run --rm -ti  -v "$(realpath .):/app" --privileged -v "/dev/bus/usb:/dev/bus/usb" ghcr.io/ledgerhq/ledger-app-builder/ledger-app-builder:latest
```

### Install it to Ledger and with accept prompt on Ledger

For Banano:
Change COIN=banano in Makefile

For Nano:
Change COIN=nano in Makefile

For Ledger S:

```
BOLOS_SDK=$NANOS_SDK make load
```

---

For Ledger S+:

```
BOLOS_SDK=$NANOSP_SDK make load
```

---

For Ledger X:

```
BOLOS_SDK=$NANOX_SDK make load
```

---

### You can now use Ledger device with Nault for Nano/TheBananoStand for Banano, remember to enable auto-receive for this fix to work!
