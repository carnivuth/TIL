---
id: GIT_HOOKS
aliases: []
tags: []
index: 3
---

# GIT HOOKS

Git hooks are a special git feature that allow for script execution when some particular event is fired.

To create a git hook create a script with the name of the event that should fired the script inside the `.git/hooks` directory, some examples are already put there by git.

```bash
ls .git/hooks/
post-commit
```

## RUN HOOK ON SPECIFIC CHANGES ON FILES

In order to run hooks only when specific files are modified git cli can be used, here and example with the `post-commit` hook

```bash
#!/bin/bash
# Redirect output to stderr.
exec 1>&2
# check if last commit contains something that has notes in the name
INCLUDED=notes
if git diff --name-only HEAD HEAD~1 | grep "$INCLUDED"; then
# do something
else
  echo "no $INCLUDED modified, nothing to do"
fi
```

[PREVIOUS](pages/bash_automation/SETUP_HETZNER_STORAGEBOX_BACKUP.md) [NEXT](pages/git_github/CREATE_CI_GITHUB_ACTIONS.md)
