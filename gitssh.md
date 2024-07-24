# Setting up git using SSH

Refer to *[README](https://github.com/sylvanplot/reference-guide/)* for a description of the repository.  
This guide covers setting up a git repository from a clean machine using SSH for authentication and verification.  
This makes it possible to use git commands without having to constantly input user and password, while also signing commits to verify the user's identity (using GitHub verification feature).

# Requirements

- Having git installed. Refer to *[Git Download page](https://git-scm.com/downloads)* for an appropriate version.
- Having created a SSH key. Refer to *[Generating a new SSH key and adding it to the ssh-agent (Generating a new SSH key section)](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)*
- Having added the created SSH keys to your GitHub account. Refer to *[Adding a new SSH key to your GitHub account (Adding a new SSH key to your account section)](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)*
    > Note that SSH will be used both for authenticating and signing commits, so this step needs to be done twice, once for authentication key and another for signing key. The same public key may be used for both actions, for simplicity.
- Activating "Vigilant mode" on GitHub to check for verified commits. Refer to *[Displaying verification statuses for all of your commits (Emabling viginalt mode section)](https://docs.github.com/en/authentication/managing-commit-signature-verification/displaying-verification-statuses-for-all-of-your-commits)*
- Having an existing repository for setting up git and validating SSH connection.

# Step-by-step Guide

- Open Git Bash.

- Clone your repository using ssh syntax.

    > git clone git@github.com:USER/REPOSITORY.git

- Enter the created directory.

- Configure git username and email. Use the same username and email from your GitHub account, otherwise GitHub will not know it's you. Note that using "--global" will apply the configuration globally. If using for a specific repository, simply omit "--global" and the configuration will only apply for the current repository. Useful when working on projects across multiple platforms.

    > git config --global user.name "username"  
    > git config --global user.email "user@email.com"

- Configure git to use SSH for signing.

    > git config --global gpg.format ssh

- Configure your public key for signing. If using the default path for the public key, it will be "~/.ssh/id_rsa.pub", with no quotation marks.

    > git config --global user.signingkey PATH_PUBLIC_KEY

- Make a change and use -S for the commit so it sends your signing key for verification.

    > git commit -S -m "test SSH verification"

- Check your commit on GitHub and verify whether it says "Verified". *[Example](https://github.com/sylvanplot/reference-guide/commit/e693a323d94f49ddb8f14c77bcc1ba1cd8e13d18)*.

# References

1. *[Generating a new SSH key and adding it to the ssh-agent | Github Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)*
2. *[Adding a new SSH key to your GitHub account | Github Docs](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)*
3. *[Displaying verification statuses for all of your commits | Github Docs](https://docs.github.com/en/authentication/managing-commit-signature-verification/displaying-verification-statuses-for-all-of-your-commits)*
4. *[Telling Git about your signing key | Github Docs](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)*
5. *[Signing commits | Github Docs](https://docs.github.com/en/authentication/managing-commit-signature-verification/signing-commits)*