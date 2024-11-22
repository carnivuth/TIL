---
inde: "8"
---
# CONFIGURE PASS FOR PASSWORD STORAGE

`pass` is a handy program to manage passwords locally to a specific environment, it basically manage a local directory of text files encrypted with `gpg`

in order to create the pass subfolders a `gpg` key is needed

```bash
gpg --full-gen-key
```

- then `pass` can be initialized with the id of the key generated

```bash
  pass init "[gpg_id]"
```

- key can be added like this

```bash
pass edit [path/to/file]
```

the command creates a subdirectory under the `.password_store` folder and opens vim to edit the password content

folder structure can be showed with the `pass list` command

## GIT CONFIGURATION

`pass` can be configured to store history of the folder with `git` so to maintain the password history

```bash
 pass git init
```

### PUSHING TO REMOTE (*GITHUB*)

the git repository can be synced with a remote server as shown with github here as an example

```bash
cd ~/.password-store
gh repo create --source=. --private [repo-name]
git push --set-upstream origin main
```
 [NEXT](pages/bash_automation/CREATE_CRON_JOB.md)
