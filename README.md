# Bandit_OverTheWire

> Documentaion for the Bandit OverTheWire Levels

The Bandit wargame is aimed at absolute beginners. It will teach the basics needed to be able to play other wargames. In this level we will disscuss the solution of different levels of the Bandit wargames.

**The basic idea for the wargame is that we need to obtain the password for the next level from the current logged in user. To obtain the password we need to perform some linux commands on the Virtual Machine. The level of difficulty rises as we move to higher the levels**

Lets start with cracking the passwords!!

---

## Levels

-   [Bandit0](#bandit0)
-   [Bandit0->Bandit1](#bandit0---bandit1)
-   [Bandit1->Bandit2](#bandit1---bandit2)
-   [Bandit2->Bandit3](#bandit2---bandit3)
-   [Bandit3->Bandit4](#bandit3---bandit4)
-   [Bandit4->Bandit5](#bandit4---bandit5)
-   [Bandit5->Bandit6](#bandit5---bandit6)
-   [Bandit6->Bandit7](#bandit6---bandit7)
-   [Bandit7->Bandit8](#bandit7---bandit8)
-   [Bandit8->Bandit9](#bandit8---bandit9)
-   [Bandit9->Bandit10](#bandit9---bandit10)
-   [Bandit10->Bandit11](#bandit9---bandit10)
-   [Bandit11->Bandit12](#bandit11---bandit12)
-   [Bandit12->Bandit13](#bandit12---bandit13)

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
> -   human-readable
> -   1033 bytes in size
> -   not executable

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

## Bandit6 -> Bandit7

> **Target:** The password for the next level is stored somewhere on the server and has all of the following properties:
>
> -   owned by user bandit7
> -   owned by group bandit6
> -   33 bytes in size

The **[find](https://man7.org/linux/man-pages/man1/find.1.html)** command let us search the files with specific size constraint.
The **-user** and **-group** tags will help us to add constraints to search the required file.

```
	bandit6@bandit:~ cd /
	bandit6@bandit:~ find -user bandit7 -group bandit6 -size 33c 2>/dev/null
	./var/lib/dpkg/info/bandit7.password
	bandit6@bandit:~ cat ./var/lib/dpkg/info/bandit7.password
	XXXXXXXXXXXXXXXXX
```

> Note: the **[2>/dev/null](https://linuxhint.com/two-dev-null-command-purpose/)** used to discard anything sent to it and read the End of File (EOF)

Got the password.

---

## Bandit7 -> Bandit8

> **Target:** The password for the next level is stored in the file data.txt next to the word millionth

A **[pipe](https://linuxhint.com/what-is-pipe-in-linux/)** **'|'** is a form of redirection of data which helps to combine multiple commands.

The output of the 1st command is the input for the 2nd command. The **[grep](https://man7.org/linux/man-pages/man1/grep.1.html)** command is used to match a regular expression or strings.

```
	bandit7@bandit:~ ls
	data.txt
	bandit7@bandit:~ cat data.txt | grep millionth
	XXXXXXXXXXXXXXXXX
```

Got the password

---

## Bandit8 -> Bandit9

> **Target:** The password for the next level is stored in the file data.txt and is the only line of text that occurs
> only once

the **[uniq](https://man7.org/linux/man-pages/man1/uniq.1.html)** **-u** gives us the only unique values from the file, and the **[sort](https://linuxhint.com/sort-command-in-linux-with-examples/)** command is used to sort
the data of the file.

```
	bandit8@bandit:~ ls
	data.txt
	bandit8@bandit:~ cat data.txt | sort | uniq -u
	XXXXXXXXXXXXXXXXX
```

Got the password

---

## Bandit9 -> Bandit10

> **Target:** The password for the next level is stored in the file data.txt in one of the few human-readable
> strings, preceded by several ‘=’ characters.

to search the lines with multiple ‘=’ character, we just need to search the '=' using **[grep](https://man7.org/linux/man-pages/man1/grep.1.html)** command.

```
	bandit9@bandit:~ ls
	data.txt
	bandit9@bandit:~ cat data.txt | grep =
	========== the*2i"4
	=:G e
	========== password
	<I=zsGi
	Z)========== is
	A=|t&E
	Zdb=
	c^ LAh=3G
	*SF=s
	&========== XXXXXXXXXXXXXXXXXXXXXX
	S=A.H&^
```

Got the password!

---

## Bandit10 -> Bandit11

> **Target:** The password for the next level is stored in the file data.txt, which contains base64 encoded data

The **[file](https://www.man7.org/linux/man-pages/man1/file.1.html)** command gives the file-type details of the particular file. And, the **[base64](https://linux.die.net/man/1/base64)** command can be used to decode the content of the file using **-d** tag

You can find more information about base64 **[here](https://en.wikipedia.org/wiki/Base64)**

```
	bandit10@bandit:~ ls
	data.txt
	bandit10@bandit:~ file data.txt
	data.txt: ASCII text
	bandit10@bandit:~ cat data.txt | base64 -d
	The password is XXXXXXXXXXXXXXXXXX
```

Got the password!

---

## Bandit11 -> Bandit12

> **Target:** The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

The rotation of the alphabets by 13 positions indicates that the **[rot13 encryption](https://en.wikipedia.org/wiki/ROT13)** is done.
To decrypt the data we need to use tr command with the particular alphabet sets as **N-ZA-Mn-za-m** indicating that the alphabets starts from n to z and then a to m for both upper and lower case.

```
	bandit10@bandit:~ ls
	data.txt
	bandit10@bandit:~ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
	The password is XXXXXXXXXXXXXXXXXX
```

Got the password!

---

## Bandit12 -> Bandit13

> **Target:** The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

The data.txt file is encoded in hex. To decode the file we need to create a backup folder in **/tmp/\<folder name>**. The mkdir helps us to create the desired folder. The cp command helps us to copy the file to the newly created folder.

Then, using **cd** we can go to the temporary folder. The **xxd -r** command is used to decode the data.txt into file data_hex.

The file is encrypted in multilevel with gzip, tar and bzip2, to decode the file we need to follow repeated
commands as per the file type.

```
- gzip -d \<file_name>.gz
- tar xvf \<file_name>.tar
- bzip2 -d \<file_name>.bz2
```

Then finally we will get a text file with password stored in it.

```
	bandit12@bandit:/tmp/secttp$ cat data.txt | xxd -r > data
	bandit12@bandit:/tmp/secttp$ file data
	data: gzip compressed data, was "data2.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unix
	bandit12@bandit:/tmp/secttp$
```

```
	bandit12@bandit:/tmp/secttp$ mv data3 data4.gz
	bandit12@bandit:/tmp/secttp$ gzip -d data4.gz
	bandit12@bandit:/tmp/secttp$ ls
	data4  data.txt

	bandit12@bandit:/tmp/secttp$ file data4
	data4: POSIX tar archive (GNU)bandit12@bandit:/tmp/secttp$ mv data4 data5.tar
	bandit12@bandit:/tmp/secttp$ tar -xf data5.tar
	bandit12@bandit:/tmp/secttp$ ls
	data5.bin  data5.tar  data.txt

	bandit12@bandit:/tmp/secttp$ file data5.bin
	data5.bin: POSIX tar archive (GNU)bandit12@bandit:/tmp/secttp$ mv data5.bin data6.tar
	bandit12@bandit:/tmp/secttp$ tar -xf data6.tar
	bandit12@bandit:/tmp/secttp$ ls
	data5.tar  data6.bin  data6.tar  data.txt

	bandit12@bandit:/tmp/secttp$ file data6.bin
	data6.bin: bzip2 compressed data, block size = 900kbandit12@bandit:/tmp/secttp$ mv data6.bin data7.bz
	bandit12@bandit:/tmp/secttp$ bzip2 -d data7.bz
	bandit12@bandit:/tmp/secttp$ ls
	data5.tar  data6.tar  data7  data.txt

	bandit12@bandit:/tmp/secttp$ file data7
	data7: POSIX tar archive (GNU)bandit12@bandit:/tmp/secttp$ mv data7 data8.tar
	bandit12@bandit:/tmp/secttp$ tar -xf data8.tar
	bandit12@bandit:/tmp/secttp$ ls
	data5.tar  data6.tar  data8.bin  data8.tar  data.txt

	bandit12@bandit:/tmp/secttp$ file data8.bin
	data8.bin: gzip compressed data, was "data9.bin", last modified: Tue Oct 16 12:00:23 2018, max compression, from Unixbandit12@bandit:/tmp/secttp$ mv data8.bin data9.gz
	bandit12@bandit:/tmp/secttp$ gzip -d data9.gz
	bandit12@bandit:/tmp/secttp$ ls
	data5.tar  data6.tar  data8.tar  data9  data.txt

	bandit12@bandit:/tmp/secttp$ file data9
	data9: ASCII text
	bandit12@bandit: cat data9
	XXXXXXXXXXXXXXXXXX
```

Got the password!

---
