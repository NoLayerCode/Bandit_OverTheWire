# Bandit_OverTheWire
>Documentaion for the Bandit OverTheWire Levels

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames. In this level we will disscuss the solution of different levels of the Bandit wargames.

**The basic idea for the wargame is that we need to obtain the password for the next level from the current logged in user. To obtain the password we need to perform some linux commands on the Virtual Machine. The level of difficulty rises as we move to higher the levels**

Lets start with the cracking the passwords!!

---
## Levels
- [Bandit0](#bandit0)
- [Bandit0->Bandit1](#bandit0---bandit1)

---
## Bandit0

> **Target:** The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

The above block is the target for level0.
To connect to the server we need to use **SSH** command which helps us to connect any server with port **22** unless we specify the custom port to connect.

You can find more information about SSH command [here](https://man7.org/linux/man-pages/man1/ssh.1.html).

```
    ssh user@dns/ip -p port
```
This is basic syntax for ssh command. Using the following configuration data we can login to the server

```
    User: bandit0 
    host: bandit.labs.overthewire.org
    password: bandit0
    port: 2220
```
```
    $ ssh bandit0@bandit.labs.overthewire.org -p 2220
    This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

    bandit0@bandit.labs.overthewire.org's password: bandit0
```
Using the above command we are able to login to the server. Now we need to crack the command for next level in Bandit1 level

## Bandit0 -> Bandit1

> **Target:** The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Once logged in to the server we need to find the **readme** file to find the password. 

We can use the **[ls](https://en.wikipedia.org/wiki/Ls)** linux command to get the list of all files and directories of the current directory.
```
    bandit0@bandit:~$ ls
    readme
```
Now we need to display the content of the file. For that we can use **[cat](https://en.wikipedia.org/wiki/Cat_(Unix))** command.
```
    bandit0@bandit:~ cat readme
    XXXXXXXXXXXXXXXX
```
Got the password for Level2.

