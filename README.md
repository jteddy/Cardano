# Cardano Node

### Initial System Configuration

**Update the system**

```bash
sudo apt-get update -y
sudo apt-get upgrade -y
```

**Install needed tools**

```bash
sudo apt-get install -y vim net-tools curl apt-utils nano locate
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
./guild-deploy.sh -b master -n preview -t cnode -s pblmdcowxfs
```

**Checks**

```bash
cardano-cli version
cardano-node version
```

**Update port number or pool name for relative paths**

```bash
CNODEBIN="${HOME}/.local/bin/cardano-node"
CCLI="${HOME}/.local/bin/cardano-cli"
```

```bash
vi $CNODE_HOME/scripts/env

CNODE_PORT=6000
POOL_NAME="My-Pool"
```

 If the `<MITHRIL_DOWNLOAD>` variable is set to 'Y' it will download the latest snapshot from a Mithril aggregator to speed up the blockchain synchronization. The script contains a user-defined variable `CPU_CORES` which determines the number of CPU cores the node will use upon start-up:

```bash
vi $CNODE_HOME/scripts/cnode.sh
```

**Find and Edit the Variable**: Once the file is open in vim, you need to search for the CPU_CORES variable. Press / to enter search mode, type CPU_CORES, and press Enter to find the line:

```bash
#CPU_CORES=4            # Number of CPU cores cardano-node process has access to (please don't set higher than physical core count, 4 recommended)
```

Show the number of cores on the system

```bash
lscpu -p | grep -v '#' | sort -u -t, -k 2,4 | wc -l
```

**Test**

Test the server in interactive mode.

```bashcd "${CNODE_HOME}"/scripts
cd "${CNODE_HOME}"/scripts
./cnode.sh
```

#### Modify the node's config files

```bash
vi $CNODE_HOME/files/config.json
```



```bash
 vi $CNODE_HOME/files/topology.json
```

Update the "*description*" in that config file.

Test Again

```bash
cd "${CNODE_HOME}"/scripts
./cnode.sh
```

#### Start the submit-api

Change the

- HOSTADDR
- HOSTPORT

```bash
vi $CNODE_HOME/scripts/submitapi.sh
```

Test by executing ./submitapi.sh

### Add as SystemD





# Firewall Configuration

If you are using port  6000    for your node, make sure it’s open on your server:
```bash
sudo ufw allow 6000/tcp
sudo ufw reload
```
**NTP Firewall Configuration**
```bash
sudo ufw allow ntp
sudo ufw reload
```

# Grafana Monitoring

