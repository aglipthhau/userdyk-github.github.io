---
layout : post
title : PL00, System programming
categories: [PL00]
comments : true
tags : [PL00]
---
[Back to the previous page](https://userdyk-github.github.io/Study.html) <br>
List of posts to read before reading this article
- <a href='https://userdyk-github.github.io/'>post1</a>
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

## Contents
{:.no_toc}

* ToC
{:toc}

<hr class="division1">

## **Introduction**

### ***File on Linux***

<br><br><br>

### ***Process on Linux***

<br><br><br>

### ***Authority on Linux***

- OS manages permissions of users and resources
- Linux manages permissions with users and groups
- root is super user(manager)
- On each files, for owner, owner group, and all users
    - management of 'read', 'write', 'execute'
    - save access authority information in data structure of inode

<br><br><br>

<hr class="division2">

## **Shell**

### ***Multiuser system***

<span class="frame3">current user name accessed on linux</span>
```bash
$ whoami
```
<br><br><br>

<span class="frame3">set password</span>
```bash
passwd [user_name]
```
<details markdown="1">
<summary class='jb-small' style="color:blue">when error</summary>
<hr class='division3'>
<a href="https://www.codevoila.com/post/26/fix-authentication-token-manipulation-error-when-changing-user-password-in-ubuntu" target="_blank">https://www.codevoila.com/post/26/fix-authentication-token-manipulation-error-when-changing-user-password-in-ubuntu</a>
```bash
$ mount -rw -o remount /
# or
$ mount -o remount,rw /
```
```bash
$ ls -l /etc/shadow
```
<details markdown="1">
<summary class='jb-small' style="color:red">OUTPUT</summary>
<hr class='division3_1'>
```
-rw-r----- 1 root shadow 1025 Feb  11 22:11 /etc/shadow
```
<hr class='division3_1'>
</details>
<br>
```bash
$ passwd
```
<hr class='division3'>
</details>
<br><br><br>

<span class="frame3">create another user id on linux</span>
```bash
$ adduser [user_name]
```
<details markdown="1">
<summary class='jb-small' style="color:blue">If you concretely create user id, setting details of user</summary>
<hr class='division3'>
```bash
$ useradd [user_name]
```
<hr class='division3'>
</details>
<br><br><br>

<span class="frame3">change user</span>
```bash
$ su [user_name]        # change id including my present .bashrc, .profile files.
$ su - [user_name]       # change id excluding my present .bashrc, .profile files.
```
<br><br><br>

<span class="frame3">authorize user</span>
```bash
:~$ cd /etc
:/etc$ vim sudoers       # change id excluding my present .bashrc, .profile files.
```
<details markdown="1">
<summary class='jb-small' style="color:blue">Edit</summary>
<hr class='division3'>
```vim
root    ALL=(ALL:ALL) ALL
```
![image](https://user-images.githubusercontent.com/52376448/68069209-833e3e80-fda0-11e9-8279-47d6d5ee45a4.png)

```vim
root    ALL=(ALL:ALL) ALL
[username]    ALL=(ALL:ALL) ALL
```
![image](https://user-images.githubusercontent.com/52376448/68069219-a9fc7500-fda0-11e9-98c7-8c3c07f60cc2.png)
<hr class='division3'>
</details>
<br><br><br>

<span class="frame3">working directory</span><br>
```bash
$ pwd
```
```bash
$ cd ~     # move user directory
$ cd /     # move root directory
$ cd -     # move previous working directory
```
```bash
$ ls
$ ls -l
$ ls -a
$ ls -al
```
<details markdown="1">
<summary class='jb-small' style="color:blue">ls wildcard example</summary>
<hr class='division3'>
![image](https://user-images.githubusercontent.com/52376448/68069411-2bed9d80-fda3-11e9-873a-478c2625db18.png)

```bash
$ ls host*
```
```
host.conf  hostname  hosts  hosts.allow  hosts.deny
```
<br>
```bash
$ ls host?
```
```
hosts
```
<hr class='division3'>
</details>
```bash
$ grep [pattern] [file_name]         # search conformable pattern(string) in file
$ grep [pattern] *                   # search conformable pattern(string) only in present directory

$ grep -i [pattern] [file_name]      # search conformable pattern(string) in file, regardless of capital and small letter
$ grep -v [pattern] [file_name]      # search unconformable pattern(string) in file
$ grep -n [pattern] [file_name]      # search conformable pattern(string) in file, numbering line on results for searching
$ grep -l [pattern] [file_name]      # search conformable pattern(string) in file, displaying only file name including pattern

$ grep -c [pattern] [file_name]      # search conformable pattern(string) in file, displaying the number of consistant pattern line on a file 
$ grep -c [pattern] *                # search conformable pattern(string) in file, displaying the number of consistant pattern line on present directory 
$ grep -c [pattern] [folder_name]    # search conformable pattern(string) in file, displaying the number of consistant pattern line per file on a folder

$ grep -r [pattern] *                # search conformable pattern(string) in present directory including sub-directory
$ grep -E "[pattern_1]|[pattern_2]|[pattern_3]" [file_name]        # search pattern 1 or pattern 2 or pattern 3 in file
```
<details markdown="1">
<summary class='jb-small' style="color:blue">grep example</summary>
<hr class='division3'>
<a href="https://recipes4dev.tistory.com/157" target="_blank">URL</a>
<hr class='division3'>
</details>


```bash
$ find 
```
```bash
$ cat [file_name]
$ head [file_name]
$ more [file_name]      # spacebar : next page
                        # enter : next line
$ tail [file_name]
```
```bash
$ rm [file_name]
$ rm -rf [folder_name]
```
<br><br><br>

<span class="frame3">file permission</span> ｜ <a href="https://en.wikipedia.org/wiki/Chmod" target="_blank" class="jb-medium">URL</a><br>
<span class="frame3_1">for file</span>
```bash
$ chmod u=rwx, g=rw, o=rx [file_name]
$ chmod 765 [file_name]
```
<span class="frame3_1">for folder</span>
```bash
$ chmod u=rwx, g=rw, o=rx [folder_name]
$ chmod -R u=rwx, g=rw, o=rx [folder_name]

$ chmod 765 [folder_name]
$ chmod -R 765 [folder_name]
```
<br><br><br>

<span class="frame3">change owner</span><br>
<span class="frame3_1">for file</span><br>
```bash
$ chown [owner:owner_group] [file_name]

$ chown [owner:] [file_name]

$ chown [:owner_group] [file_name]
$ chgrp [owner_group] [file_name]
```
<br>
<span class="frame3_1">for folder</span><br>
```bash
$ chown [owner:owner_group] [folder_name]
$ chown -R [owner:owner_group] [folder_name]

$ chown [owner:] [folder_name]
$ chown -R [owner:] [folder_name]

$ chown [:owner_group] [folder_name]
$ chown -R [:owner_group] [folder_name]
$ chgrp [owner_group] [folder_name]
$ chgrp -R [owner_group] [folder_name]
```

<br><br><br>

---

### ***Standard Stream***

<a href="https://en.wikipedia.org/wiki/Redirection_(computing)" target="_blank" style="font-size: 70%;">URL</a>

- <b>0 : stdin</b> : standard input stream from keyboard
- <b>1 : stdout</b> : standard output stream to screen
- <b>2 : stderr</b> : standard error stream to screen

```bash
$ echo [arbitary_stdout]
```
```
arbitary_stdout
```
<br><br><br>

#### Redirection

<div style="font-size: 70%;">redirection(>,<) change stream's direction for a process</div>

```bash
$ [command] > [file_name]        # overwrite with stdout
$ [command] 1> [file_name]       # overwrite with stdout
$ [command] 2> [file_name]       # overwrite with stderr

$ [command] >> [file_name]       # add text of stdout at the end
$ [command] 1>> [file_name]      # add text of stdout at the end
$ [command] 2>> [file_name]      # add text of stderr at the end

$ [command] 1>&2                 # stdout to stderr
$ [command] 2>&1                 # stderr to stdout
$ [command] >& [file_name]       # overwrite with stdout and stderr

$ [command] < [file_name] 
$ [command] < [file_name_1] > [file_name_2]
```

<br><br><br>

#### Pipe

<div style="font-size: 70%;">pipe(|) connect a process to another process</div>

```bash
:/etc$ ls | grep issue
```
```
issue
issue.net
```
<br><br><br>

---

### ***Process and Binary***

#### background

```bash
$ ./[file_name] &
$ jobs
$ bg [number_of_stoped_process]
```
<br><br><br>

#### foreground

- <b>ctrl + c</b> : terminate process
- <b>ctrl + z</b> : puase process

<br><br><br>
<hr class="division2">

## **Key factors on system programming**

### ***System call***

<br><br><br>

---

### ***API***

<br><br><br>

---

### ***ABI and Standard***

<br><br><br>

<hr class="division2">

## **Management of process**

<br><br><br>

<hr class="division2">

## **IPC, Inter-Process Communication**

<br><br><br>

<hr class="division2">

## **Signal action**

<br><br><br>

<hr class="division2">

## **Shell script**

<br><br><br>

<hr class="division2">

## **Thread**

<br><br><br>

<hr class="division2">

## **System programming**

<br><br><br>

<hr class="division2">

<hr class="division1">

List of posts followed by this article
- [post1](https://userdyk-github.github.io/)
- <a href='https://userdyk-github.github.io/'>post2</a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

Reference
- <a href='' target="_blank"></a>
- <a href='https://userdyk-github.github.io/'>post3</a>

---

<details markdown="1">
<summary class='jb-small' style="color:blue">OUTPUT</summary>
<hr class='division3'>

<hr class='division3'>
</details>


