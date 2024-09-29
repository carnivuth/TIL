# SETUP BACKUP WITH HETZNER STORAGEBOX

Hetzner is a cloud provider that offers various services, Paas and Saas and also cloud storage, in the form of storageboxes, in order to configure a backup for a new host

- create a storagebox subaccount to limit the user privileges of the backupped guest only to it's own files

- create `.ssh` directory 
- create ssh keys for the storage box
- copy pubkey to remote
- setup ssh config 

```bash
Host storagebox-address
    User subuser
    IdentityFile ~/.ssh/id_rsa
    Port 23
```

- setup sync script with remote 

```bash
#!/bin/bash
DEPS="rsync"
DATASTORES="" # PATHS to folders to sync with remote
REMOTE="" # REMOTE URL to storagebox
NTFY_ENDPOINT="" # NTFY ENDPOINT for notifications
HEALTHCHECKS_ENDPOINT="" # HEALTHCHECKS ENDPOINT for notifications

for datastore in $DATASTORES; do
if rsync -Pavr "$datastore" "$REMOTE:"; then
        curl  "$HEALTHCHECKS_ENDPOINT"
        curl "$NTFY_ENDPOINT" -X POST  -d "done sync from $HOSTNAME to $REMOTE of $datastore"
else
        curl "$NTFY_ENDPOINT" -X POST  -d "BROKEN  sync from $HOSTNAME to $REMOTE of $datastore"
fi
done
```