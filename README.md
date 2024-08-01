<h1 align="center">
  How to Use Multiple GitHub Accounts
</h1>
If you have multiple GitHub accounts, it can be a challenge to manage them on the same computer. Fortunately, with a few configuration changes, you can easily use multiple GitHub accounts.

Here are the steps to set up multiple GitHub accounts:

### **1. Generate SSH keys for each account**

First, you need to generate SSH keys for each GitHub account you want to use. You can use the following command to generate an SSH key for your "Account 1" GitHub account:

```bash
ssh-keygen -t ed25519 -C "your_personal_email@example.com" -f ~/.ssh/id_ed25519_personal

ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

Be sure to replace <mark>**_your-email@example<sub>▪</sub>com_**</mark> with the email address associated with your "Account 1" GitHub account. When prompted, save the SSH key to the default location (~/.ssh/id_rsa).

Repeat this process for each GitHub account you want to use, using a unique name for each SSH key (e.g., **id_rsa_account1** for "Account 1", **id_rsa_account2** for "Account 2", etc.).

### **2. Add SSH keys to GitHub**

Next, you need to add the SSH keys to each GitHub account. Log in to your "Account 1" GitHub account and go to the "Settings" page. Click on the "SSH and GPG keys" tab, then click the "New SSH key" button. Paste the contents of the id_rsa_account1.pub file (located in ~/.ssh/) into the "Key" field and give the key a descriptive name. Click "Add SSH key" to save the key.

Repeat this process for each GitHub account you want to use, using the appropriate SSH key for each account.

### **3. Create a configuration file**

Next, you need to create a configuration file for SSH to specify the different hosts and SSH keys to use for each GitHub account. Use the following command to create a new configuration file (or open the existing one if it already exists):

```bash
nano ~/.ssh/config
```

In the configuration file, add the following lines for each GitHub account you want to use:

```bash
# Account 1
Host github.com-account1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account1

# Account 2
Host github.com-account2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_account2
```

Replace "account1" and "account2" with unique names for each GitHub account. Make sure that the IdentityFile parameter points to the correct SSH key for each account.

### **4. Clone repositories and set up the remote origin**

Next, you need to clone the repositories you want to work with using Git. For each GitHub account, follow these steps:

1. Open a terminal window and navigate to the directory where you want to clone the repository.

2. Use the following command to clone the repository from the corresponding GitHub account:

```bash
git clone git@github.com-account1:<account1-username>/<repository-name>.git
```

Replace `<account1-username>` with the username of your "Account 1" GitHub account, and `<repository-name>` with the name of the repository you want to clone.

<center>It's important to note that I made a mistake <br> initially by not using the Git hostname correctly <br> for my personal account. I was using the <br> following incorrect command:</center> <br>

```bash
git clone git@github.com<account1-username>/<repository-name>.git
```

<center>By omitting the correct hostname, I was <br> experiencing "access denied" errors when <br> fattempting to push or pull. Even though I had <br> deleted all my GitHub credentials, it was still <br>using my work Git account. </center> <br>

<center>
To avoid this mistake, make sure to use the <br>
correct format with the Git hostname specified <br>
as follows:
</center>

```bash
git clone git@github.com-account1:<account1-username>/<repository-name>.git
```

<center>
By using the correct hostname, you ensure that <br>
Git correctly associates the repository with the <br>
respective GitHub account.
</center> <br>

Repeat this process for each GitHub account and repository you want to work with.

### **5. Associate existing local code with the remote origin**

If you already have existing code on your local machine that you want to associate with your GitHub accounts, you can follow these steps:

- Navigate to the local repository directory using the command line:

```bash
cd /path/to/repository
```

- Use the following command to view the current remote URLs associated with the repository:

```bash
git remote -v
```

This command will display the current remote origin URL.

- To update the remote origin URL for the specific GitHub account, use the following command:

```bash
git remote set-url <account-remote-name> <repository-url>
```

Replace `<account-remote-name>` with the name you assigned to the remote repository for the corresponding GitHub account, and `<repository-url>` with the URL of the repository.

For example, if you want to update the remote origin URL for "Account 1", you can use:

```bash
git remote set-url account1 git@github.com-account1:<account1-username>/<repository-name>.git
```

- Verify that the remote origin URL has been updated by running the following command:

```bash
git remote -v
```

The new remote URL should be displayed.

By following these steps, you can associate your existing local code with the appropriate remote origin URL for each GitHub account. This ensures that you can push and pull changes to the correct remote repository associated with the respective account.
