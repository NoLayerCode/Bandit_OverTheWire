# Bandit_OverTheWire

> Documentaion for the Bandit OverTheWire Levels

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames. In this level we will disscuss the solution of different levels of the Bandit wargames.

**The basic idea for the wargame is that we need to obtain the password for the next level from the current logged in user. To obtain the password we need to perform some linux commands on the Virtual Machine. The level of difficulty rises as we move to higher the levels**

Lets start with cracking the passwords!!

---

## Levels

- [Bandit0](#bandit0)
- [Bandit0->Bandit1](#bandit0---bandit1)
- [Bandit1->Bandit2](#bandit1---bandit2)
- [Bandit2->Bandit3](#bandit2---bandit3)
- [Bandit3->Bandit4](#bandit3---bandit4)
- [Bandit4->Bandit5](#bandit4---bandit5)
- [Bandit5->Bandit6](#bandit5---bandit6)

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

---

## Bandit0 -> Bandit1

> **Target:** The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Once logged in to the server we need to find the **readme** file to find the password.

We can use the **[ls](https://en.wikipedia.org/wiki/Ls)** linux command to get the list of all files and directories of the current directory.

```
	bandit0@bandit:~$ ls
	readme
```

Now we need to display the content of the file. For that we can use **[cat](<https://en.wikipedia.org/wiki/Cat_(Unix)>)** command.

```
	bandit0@bandit:~ cat readme
	XXXXXXXXXXXXXXXX
```

Got the password for Level2.

---

## Bandit1 -> Bandit2

> **Target:** The password for the next level is stored in a file called - located in the home directory

Now we need to login using the password we got in last level and following details.

```
	ssh: ssh bandit1@bandit.labs.overthewire.org -p 2220
	user: bandit1
	password: XXXXXXXXXXX(the one you got in last level)
```

The - character creates missuderstaning with **stdin/stdout** i.e. dev/stdin or dev/stdout. Thus, to open the files starting with [special characters](https://tldp.org/LDP/abs/html/special-chars.html) we need to follow below approch. Instead of using `cat ./-` we can also use `cat < -`.

```
	bandit1@bandit:~ cat ./-
	XXXXXXXXXXXXXXXX
```

Got the password!

---

## Bandit2 -> bandit3

> **Target:** The password for the next level is stored in a file called spaces in this filename located in the home directory

First we will login using **ssh** command.
To access the files with spaces in the filename, we need to use the **\\** escape character as shown below

for more information click [here](https://linuxhint.com/reference-filename-with-spaces-linux/).

```
	bandit2@bandit:~ cat spaces\ in\ this\ filename
	XXXXXXXXXXXXXXXX
```

Got the password.

## Bandit3 -> Bandit4

> **Target:** The password for the next level is stored in a hidden file in the inhere directory.

The **cd** command is used to change the directory.The hidden file can be displayed using **ls -la or ls -a** command, and as shown in the code. We can use **.<file_name>** as prefix to display the content. The '.' indicated that the file is hidden in
the directory.

```
	bandit3@bandit:~ cd inhere
	bandit3@bandit:~ ls -la
	total 12
	******* bandit4 bandi3 ** *** *** .hidden
	bandit3@bandit:~ cat .hidden
	XXXXXXXXXXXXXXXXX
```

We got password of next level.

---

## Bandit4 -> Bandit5

> **Target:** The password for the next level is stored in the only human-readable file in the inhere directory.
>
> Tip: if your terminal is messed up, try the “reset” command.

To print the file starting with **'-'** , we need to add **'./'** as prefix of the file name.
But doing this is quite draggy and worn-out process for every file.

Instead of that we can use **[file](https://man7.org/linux/man-pages/man1/file.1.html)** command to find the filetype of the files.

```
	bandit4@bandit:~ cd inhere
	bandit4@bandit:~ file *
	-file00: data
	-file01: data
	-file02: data
	-file03: data
	-file04: data
	-file05: data
	-file06: data
	-file07: ASCII text
	-file08: data
	-file09: data
```

Now we know that only **-file07** is human-readable. So, we just need to display its content and we will get the password for the next level.

```
	bandit4@bandit:~ cat ./-file07
	XXXXXXXXXXXXXXXXX
```

Got the password!

---

## Bandit5 -> Bandit6

> **Target:** The password for the next level is stored in a file somewhere under the inhere directory and has
> all of the following properties:
>
> - human-readable
> - 1033 bytes in size
> - not executable

The **[find](https://man7.org/linux/man-pages/man1/find.1.html)** command let us search the files with specific size constraint.

The _-size_ flag is used to specify the required filesize, and in **1033c** the _c_ denotes that the size is in _bytes_.

```
	bandit5@bandit:~ cd inhere
	bandit5@bandit:~ find . -size 1033c
	./mybehere07/.file02
	bandit5@bandit:~ cat ./mybehere07/.file02
	XXXXXXXXXXXXXXXXX
```

> Note: the **.** in find command indicates to search the current directory.s

Got the password.

---
