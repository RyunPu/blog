---
layout: post
title:  "Generate a new SSH key and add it to the ssh-agent"
date:   2018-07-13
categories: ['web development']
tags: ['git']
---

### Generate a new SSH key

1. Open Terminal.

2. Paste the text below, substituting in your GitHub email address.

```bash
$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This creates a new ssh key, using the provided email as a label.

```bash
> Generating public/private rsa key pair.
```

3. When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

```bash
> Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]
```

4. At the prompt, type a secure passphrase. For more information, see "Working with SSH key passphrases".

```bash
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

### Add your SSH key to the ssh-agent

1. Start the ssh-agent in the background.

```bash
$ $ eval "$(ssh-agent -s)"
> Agent pid 59566
```

2. If you're using macOS Sierra 10.12.2 or later, you will need to modify your `~/.ssh/config` file to automatically load keys into the ssh-agent and store passphrases in your keychain.

```
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

3. Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.

```bash
$ ssh-add -K ~/.ssh/id_rsa
```

4. [Add the SSH key to your GitHub account](https://help.github.com/en/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account).

see more: [Connecting to GitHub with SSH](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
