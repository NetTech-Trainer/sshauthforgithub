# sshauthforgithub
# GitHub SSH Authentication Setup

## Overview

SSH authentication allows you to securely connect your local machine to GitHub without entering your username and password every time you push or pull code. Instead, it uses a pair of cryptographic keys:

* **Private Key** – stored securely on your system
* **Public Key** – uploaded to your GitHub account

Once configured, Git operations such as `clone`, `push`, and `pull` can be performed securely using SSH.

---

# Step 1: Check for Existing SSH Keys

First check if your system already has SSH keys.

```bash
ls -al ~/.ssh
```

Look for files like:

```
id_rsa
id_rsa.pub
id_ed25519
id_ed25519.pub
```

If they exist, you can reuse them.

---

# Step 2: Generate a New SSH Key

It is recommended to use the **ed25519** algorithm.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Example:

```bash
ssh-keygen -t ed25519 -C "sagar@gmail.com"
```

When prompted:

```
Enter file in which to save the key (/home/user/.ssh/id_ed25519):
```

Press **Enter** to accept the default location.

You may optionally set a **passphrase** for additional security.

After generation, two files will be created:

```
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

* `id_ed25519` → Private Key
* `id_ed25519.pub` → Public Key

---

# Step 3: Start SSH Agent

Start the SSH agent:

```bash
eval "$(ssh-agent -s)"
```

Add the private key to the SSH agent:

```bash
ssh-add ~/.ssh/id_ed25519
```

---

# Step 4: Copy the Public Key

Display the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Example output:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIEXAMPLEKEY sagar@gmail.com
```

Copy the entire key.

---

# Step 5: Add SSH Key to GitHub

1. Log in to GitHub
2. Go to **Settings**
3. Select **SSH and GPG Keys**
4. Click **New SSH Key**
5. Paste your public key
6. Save the key

---

# Step 6: Test the SSH Connection

Run the following command to verify authentication:

```bash
ssh -T git@github.com
```

Expected output:

```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

# Step 7: Clone a Repository Using SSH

Instead of using HTTPS:

```
https://github.com/user/repository.git
```

Use the SSH URL:

```
git@github.com:user/repository.git
```

Clone the repository:

```bash
git clone git@github.com:user/repository.git
```

---

# Troubleshooting

## Permission Denied (publickey)

If you get this error:

```
Permission denied (publickey)
```

Try adding the key again:

```bash
ssh-add ~/.ssh/id_ed25519
```

Also ensure the public key is added to your GitHub account.

---

# Advantages of SSH Authentication

* No need to enter password repeatedly
* Secure cryptographic authentication
* Ideal for automation and CI/CD
* Faster Git operations

---

# Conclusion

SSH authentication provides a secure and efficient way to interact with GitHub repositories. Once configured, it simplifies daily Git workflows such as cloning, pushing, and pulling code.

---
