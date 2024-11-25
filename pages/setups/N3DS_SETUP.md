# NINTENDO 3DS DEFINITIVE CONFIGURATION GUIDE

My personal ultimate guide to setup a bullet proof nintendo 3ds emulator machine

- follow the ultimate guide to [mod 3ds](https://3ds.hacks.guide/)

after modding the 3ds configure network copy the [Universal Updater](https://universal-team.net/projects/universal-updater) cia in the sd and install it

- download `twilight menu` from Universal updater
- download `ftpd` menu from Universal updater

- copy roms on the sd card

## SETUP SAVES BACKUP

- set static ip in the 3ds configuration (`or DHCP reservation on router`)

configure a container with the following cronjob:

- install ftp

```bash
apt install ftp
```

- write the following script in `/usr/local/bin/backup_3ds.sh`

```bash
#!/bin/bash
PORT=5000
SERVER=192.168.1.28
NDS_DEST=/var/lib/nds_saves; if [[ ! -d "$NDS_DEST" ]]; then mkdir -p "$NDS_DEST"; fi
GBA_DEST=/var/lib/gba_saves; if [[ ! -d "$GBA_DEST" ]]; then mkdir -p "$GBA_DEST"; fi
if nc -z -w1 "$SERVER" "$PORT"; then
    echo "FTP is up."
    ftp -n -p "$SERVER" "$PORT" <<EOF
    binary
    lcd "$NDS_DEST"
    cd roms/nds/saves
    mget *
    lcd "$GBA_DEST"
    cd roms/gba/saves
    mget *
EOF
    echo DONE
else
    echo "FTP is down. Will try again."
fi
```

- add cronjob

```bash
*/5 * * * * /usr/local/bin/backup_3ds.sh >> /var/log/backup_3ds.sh 2>&1
```
