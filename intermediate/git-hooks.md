---
title: "Introduction to Git Hooks"
subtitle: Enhance Your Workflow with Automation and Customization Techniques for Improved Code Quality and Efficiency with Git Hooks.
slug: introduction-to-git-hooks
tags: git, version control, automation, workflow, software development, git hooks, hooks
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1718106078151/u6WzSQFCX.webp?auto=format
domain: 10xdev.codeparrot.ai
saveAsDraft: false
---

Git Hooks are scripts that run automatically before or after certain Git commands. They are a powerful tool that can help you automate tasks, enforce coding standards, and improve your workflow. This article will introduce you to Git Hooks and show you how to use them to enhance your development process.

## What are Git Hooks?

Git Hooks are scripts that Git runs before or after certain commands. They are stored in the `.git/hooks` directory of your Git repository and are executed automatically when you run a Git command. There are several types of Git Hooks, each corresponding to a different command or event in the Git workflow.

Pre-commit hooks, for example, run before you commit changes to your repository. They can be used to enforce coding standards, run tests, or perform other tasks to ensure the quality of your code. Post-commit hooks, on the other hand, run after you commit changes and can be used to send notifications, update issue trackers, or perform other tasks.

These hook scripts are only limited by your imagination and can be used to automate almost any task you can think of. They are a powerful tool that can help you improve your workflow, enforce best practices, and save time.

## How to Use Git Hooks

To use Git Hooks, you need to create a script and save it in the `.git/hooks` directory of your Git repository. The script should be named after the hook you want to use (e.g., `pre-commit`, `post-commit`, etc.) and should be executable and should have appropriate permissions (e.g., `chmod +x pre-commit`).

Here is a full list of the available Git Hooks:

- `applypatch-msg`: Executes before a patch is applied, to edit the patch's commit message.

- `pre-applypatch`: Runs before a patch is applied, useful for verifying patch integrity.

- `post-applypatch`: Executes after a patch is applied, typically used for notifications.

- `pre-commit`: Runs before the commit process starts, often used for linting or tests.

- `prepare-commit-msg`: Runs before the commit message editor is fired up, to customize the message.

- `commit-msg`: Runs after the commit message is created, for additional checks on the commit message.

- `post-commit`: Executes after a commit is completed, often used for notifications or logging.

- `pre-rebase`: Runs before the rebase process begins, useful for verifying the rebase can proceed.

- `post-checkout`: Runs after a checkout is performed, typically used to configure the working directory.

- `post-merge`: Runs after a merge is completed, commonly used for notifications or cleanup.

- `pre-receive`: Runs before a push to the server is processed, used to enforce policies.

- `update`: Runs during a push to update references, often used to enforce branch-specific policies.

- `post-receive`: Executes after a push to the server is processed, for notifications or deployment.

- `post-update`: Runs after references are updated on the server, useful for repository maintenance tasks.

- `pre-auto-gc`: Runs before automatic garbage collection, often used to prevent unwanted GC.

- `post-rewrite`: Runs after commands like git commit --amend or git rebase, for adjusting changes.

- `pre-push`: Executes before a push to a remote repository, typically used to verify the push contents.

Note that all these hooks, if present by default, are stored as `.sample` files in the `.git/hooks` directory. You have to remove the `.sample` extension to activate them and make them executable.

You can read more about these hooks [here](https://www.git-scm.com/docs/githooks) and [here](https://githooks.com/).

### Example: Pre-commit Hook

Here is an example of a simple pre-commit hook that checks for whitespace errors in your code:

```bash
#!/bin/sh

# Check if this is the initial commit
if git rev-parse --verify HEAD >/dev/null 2>&1
then
    echo "pre-commit: About to create a new commit..."
    against=HEAD
else
    echo "pre-commit: About to create the first commit..."
    against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
fi

# Use git diff-index to check for whitespace errors
echo "pre-commit: Testing for whitespace errors..."
if ! git diff-index --check --cached $against
then
    echo "pre-commit: Aborting commit due to whitespace errors"
    exit 1
else
    echo "pre-commit: No whitespace errors :)"
    exit 0
fi
```

Another example of a pre-commit hook is mentioned below. This hook validates the git config’s global user email and checks whether a gpg key exists. The hook is useful so that the commits contain the correct committer email address and also to ensure the commits are signed.

```bash
#!/bin/bash

PWD=`pwd`
globalEmail=`git config --global --get user.email`
signingKey=`git config --global --get user.signingkey`
workEmail="work@domain.com"

if [[ $PWD != "*demo*" && $globalEmail != $workEmail ]];
then
        echo "Commit email and global git config email differ"
        echo "Global commit email: "$globalEmail""
        echo "Committing email expected: $workEmail"
        exit 1
elif [[ $signingKey -eq "" ]];
then
        echo "No signing key found. Check global gitconfig"
        exit 1
else
        echo ""
        exit 0
fi
```

Remember to make the script executable by running `chmod +x pre-commit` and save it in the `.git/hooks` directory of your Git repository.

Here's what it looks like:

![Pre-commit Hook](https://cdn.hashnode.com/res/hashnode/image/upload/v1718105209761/yOj-RUdXz.png?auto=format)

Here, the pre-commit hook tries to check if the user's email address is set to a specific value. If the email address is not set to the expected value, the commit is aborted. In my case, the expected email address is `work@domain.com` but I am logged in with a different email address. So, the commit is aborted.

## Scripting languages

You can write Git Hooks in any scripting language you are comfortable with, such as Bash, Python, Ruby, or Perl. The only requirement is that the script should be executable and should have appropriate permissions.

Example of a `prepare-commit-msg` hook written in Python:

```python
#!/usr/bin/env python

import sys, os

commit_msg_filepath = sys.argv[1]
with open(commit_msg_filepath, 'w') as f:
    f.write("# Please include a useful commit message!")
```

### Example: Post-commit Hook

Here is an example of a simple post-commit hook written in Python that sends an email notification after a commit:

```python
#!/usr/bin/env python

import smtplib
from email.mime.text import MIMEText
from subprocess import check_output

# Get the git log --stat entry of the new commit
log = check_output(['git', 'log', '-1', '--stat', 'HEAD'])

# Create a plaintext email message
msg = MIMEText("Look, I'm actually doing some work:\n\n%s" % log)

msg['Subject'] = 'Git post-commit hook notification'
msg['From'] = 'mary@example.com'
msg['To'] = 'boss@example.com'

# Send the message
SMTP_SERVER = 'smtp.example.com'
SMTP_PORT = 587

session = smtplib.SMTP(SMTP_SERVER, SMTP_PORT)
session.ehlo()
session.starttls()
session.ehlo()
session.login(msg['From'], 'secretPassword')

session.sendmail(msg['From'], msg['To'], msg.as_string())
session.quit()
```

This probably isn't the best way to send email notifications from a Git Hook, but it gives you an idea of what's possible.

## Projects Using Git Hooks

Here are a few projects that use Git Hooks to automate tasks and improve workflow that are also mentioned on [githooks.com](https://githooks.com/):

- [Lolcommits](https://github.com/lolcommits/lolcommits) - Takes a snapshot with your webcam every time you git commit code, and archives a lolcat style image with it.

- [Husky](https://github.com/typicode/husky) - Git hooks for Node.js, manage your hooks from your package.json.

- [podmena](https://github.com/bmwant/podmena) - Enhance your commit messages by adding random emoji.

- [overcommit](https://github.com/sds/overcommit) - A well-maintained, up-to-date, flexible Git hook manager.

## More Resources

- [Git Hooks Documentation](https://www.git-scm.com/docs/githooks)
- [Git Hooks](https://githooks.com/)
- [Git Kraken](https://www.gitkraken.com/blog/git-hooks)
- [Atlassian Git Hooks](https://www.atlassian.com/git/tutorials/git-hooks)

## Conclusion

Git Hooks are a powerful tool that can help you automate tasks, enforce coding standards, and improve your workflow. By using Git Hooks, you can save time, improve code quality, and ensure that your team follows best practices. I hope this article has given you a good introduction to Git Hooks and inspired you to start using them in your projects.