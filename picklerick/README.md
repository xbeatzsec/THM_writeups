# PICKLERICK ROOM

Link -> https://tryhackme.com/room/picklerick

Difficulty -> Easy

------------------------------------------------

So first lets deploy the machine to attack it!

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
## 2 - Let's see that we have more directories on this web page

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



