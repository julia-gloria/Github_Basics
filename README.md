# Basic Github Repository

## Learning Basic Functionality using GitBash

This project should demonstrate a basic understanding of how to use GitBash. I really only looked at this website as a way to view software that others have made that I can incorporate into my workflow or other projects, and not as a software developer. This is my attempt to learning some of the fundamentals to using GitHub from the GitBash terminal.

## Setting up SSH

I set up the Secure Shell (SSH) protocol using GitHub's [public documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) and troubleshooted it using the same documenation. I found my issue to be that I made the authentication key signed in GitHub, when it needed to be just an Authentication Key, using the documentation on the website. Furthermore, I found myself using multiple terminals, like how GitHub suggested a PowerShell terminal for creating the SSH-agent. I found you could do it all in one GitBash terminal which is more straightforward than the docs.

## Testing Push
I know from experience in higher education that GitHub is used to push and pull files from a project in a simple and effective way, allowing for quick iteration between many different people. However, the logistics of that I have never actually had to deal with. The most I've done is contributing to certain branches in group projects that I have been apart of. Using [this](https://gist.github.com/xirixiz/b6b0c6f4917ce17a90e00f9b60566278) guide for how to commit and push a document to an existing repository, I believe I can push this file into my project.

## Troubleshooting Problems
I had some trouble getting the correct format for pushing a commit to GitHub. For my future self, this will be a helpful guide to understanding how to do it through GitBash in a way that makes sense. 

### Checking SSH Connection

#### SSH Agent Setup

This assumes you've generated an SSH key and you have it connected to your GitHub account. To check if you've set up your SSH connection properly, start an instance of the ssh-agent in GitBash in the background.

```git-bash
$ eval "$(ssh-agent -s)"
```

#### Checking the Correct Key Identity

After starting an instance of the agent, check if you have the correct key attached to your GitHub account by typing:

```git-bash
$ ssh-add -l -E sha256 
```

This should print a string of numbers and letters corresponding to the Authentication Key you setup in your GitHub account. Also make sure that your SSH key is set to Authentication Key in GitHub instead of Signed Key.

#### Test Connection

Finally to check your SSH Connection type:

```git-bash
$ ssh -T git@github.com
```

This should give you the response:

```
Hi user-name! You've successfully authenticated, but GitHub does not provide shell access.
```

If you do not get this response you should look at the GitHub's [documentation here](https://docs.github.com/en/authentication/troubleshooting-ssh/error-permission-denied-publickey). I got a permission denied error the first time doing this, and I did everything perfectly except making the SSH Key a signed key instead of an Authentication Key. For some reason the Authentication Key worked with the generated ED25519 key. Maybe an RSA key would work better, but I haven't tried that yet.

## How to Push

From my current understanding, you first need your GitBash in the working directory of the folders you. For Windows, that is using ```cd``` until you get to the working directory that you'd like to use.

Once there you can type:

```git-bash
$ git init
```

This initializes the your working directory as the master repository for the GitHub project. You only need to do this once.

Make sure that have the file you want to add in the master directory. Then type:

```git-bash
$ git add [File]
```

This will add your file to the commit. I am guessing you can add more than one file by just adding them individually, or adding entire directories the same way.

Then you can use the following to commit:

```git-bash
$ git commit -m "[message]"
```

At this point, I'm unsure of what actually allows me to push into my GitHub repository, but I am guessing it is the following:

```git-bash
$ git remote set-url origin git@github.com:user-name/repository_name.git
```

Once you have that, you should be able to:

```git-bash
$ git push
```

But I got some errors from doing this.

### Author Identity Unknown Error
``` 
Author identity unknown

*** Please tell me who you are.

Run

    git config --global user.email "you@example.com"
    git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.
```

This error occurs right after trying to ```git commit -m "[message]"```. I'm guessing this error occurs because I had put just Authentication Key instead of Signed Key for the SSH Key. Nonetheless, I was able to get around it with the error message they gave me:

So I was able to fix this issue by using my email address in the first command.

```git-bash
$ git config --global user.email "you@example.com"
``` 

### No Upstream Branch Error
```
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use
    
    git push --set-upstream origin master

To have this happen automatically for branches without a tracking upstream, 
see 'push.autoSetupRemote' in 'git help config'.
```

This error occurs after trying to ```git push```. The reason being that there is no upstream on the new repository. I basically just used the command they gave me. You can also change the config to not have to do this everytime you have a new repository, but I am not bothered by it.

```git-bash
$ git push --set-upstream origin master
```

After doing this, I successfully got my files from my working directory updated into my GitHub repository, and the markdown for the README was formatted correctly!

### Future Pushes
The problems above only seem to have occurred in the initial push and commit of my repository. Afterwards, in the same GitBash terminal, I was able to ```git add```, ```git commit```, and ```git push``` without havign to add any extra lines of code. This is good documentation for myself to reflect back on if I need to check how to setup a working directory again.

## Future Additions
I may make additional documentation for the markdown language, setting up SSH in a way that makes sense to me, and trying the RSA key instead of the ED25519 key, but for now, I am pretty confident in my abilities to be able to use this for future engineering projects.