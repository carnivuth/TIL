---
id: CREATE_CRON_JOB
aliases: []
tags: []
index: 1
---

# CREATE CRON JOB

- connect to the machine where the script should reside

- create script under `/usr/local/bin`

- create healthcheck monitoring check

## BEST PRACTICES

Common best practices to improve sysadmin operations:

- log under `var/log`
- creates temp files under `tmp`
- use the script name for logs and files in the file system
- specify dependencies in a deps variable such as `DEPS="curl git jq"`
- curl healthchecks.io for monitoring
- script should also log every possible error like `<CRITICAL_COMMAND || echo "critical command failed" >> /var/log/script_name.log>`

## SNIPPET

```bash
LOG_FILE="/var/log/<SCRIPT_NAME>.log"
<SCRIPT_NAME>_RESULT_FILE="/var/run/<SCRIPT_NAME>.result"
HEALTHCHECK="<HEALTHCHECK_URL>"

# setup result file for healthcheck
echo "0" > "$<SCRIPT_NAME>_RESULT_FILE"

# make core business

# curl healthchek.io
if [[ "$(cat "$<SCRIPT_NAME>_RESULT_FILE")" == "0" ]]; then
    curl "$HEALTHCHECK" >> "$LOG_FILE" 2>&1
fi
```

 [NEXT](pages/bash_automation/SETUP_HETZNER_STORAGEBOX_BACKUP.md)
