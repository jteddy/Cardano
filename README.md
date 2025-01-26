# Cardano Node

### Initial System Configuration

**Update the system**

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

**Install needed tools**

```bash
sudo apt-get install -y vim net-tools curl apt-utils
```
**Ensure Time Is Sync'd**

```bash
sudo apt install ntp
sudo systemctl restart ntp
```

**Test NTP**

```bash
ntpq -p
```

**Set Locale**
```bash
timedatectl set-timezone Australia/Sydney
```
**NTP Firewall Configuration**

```bash
sudo ufw allow ntp
sudo ufw reload
```

**Add User**
```bash
sudo groupadd cardano
sudo useradd -m -s /bin/bash -G cardano cardanouser
sudo usermod -aG sudo cardanouser
```

### Using Guild Operators

```bash
mkdir "$HOME/tmp";cd "$HOME/tmp"
```
```bash
curl -sS -o guild-deploy.sh https://raw.githubusercontent.com/cardano-community/guild-operators/master/scripts/cnode-helper-scripts/guild-deploy.sh
````
```bash
chmod 755 guild-deploy
```
**Run the Guild Deployment Script**

```bash
./guild-deploy.sh -b master -n prevuew -t cnode1 -s pblmdcowxfs
```

**Checks**

cardano-cli version

cardano-node version

**Update port number or pool name for relative paths**

```bash
CNODEBIN="${HOME}/.local/bin/cardano-node"
CCLI="${HOME}/.local/bin/cardano-cli"
CNODE_PORT=6000
POOL_NAME="GUILD"
```

 If the `<MITHRIL_DOWNLOAD>` variable is set to 'Y' it will download the latest snapshot from a Mithril aggregator to speed up the blockchain synchronization.

HOW TO SET THE CPU CORES??



### **Firewall Configuration**

- If you are using port  6000    for your node, make sure it’s open on your server:

  ```bash
  sudo ufw allow 6000/tcp
  sudo ufw reload
  ```

**Test**

Test the server in interactive mode.

```bashcd "${CNODE_HOME}"/scripts
cd "${CNODE_HOME}"/scripts
./cnode.sh
```
