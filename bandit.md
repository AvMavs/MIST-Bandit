# Bandit - The Writeup

#### Level 0
Well, yes, one _should_ in theory prefer a linux terminal for this. But the convenience of a GUI client is quite nice, so I used Termius, something I already use for the rest of my SSH and SFTP needs. The [website for Bandit](https://overthewire.org/wargames/bandit/bandit0.html) provides the user credentials required.

![image](https://github.com/AvMavs/Cryptonite-Bandit/assets/82929505/8a470182-20f9-48b5-97ec-1796748a5e1d)


#### Level 0 → Level 1
I used the command `ls` to list the files in the default home directory that we log in to. It only shows one file, a `readme`. I thought it was a folder and tried `cd`-ing into it, but... _yeah._ Then I went for ```nano readme``` (I know, I know, the guide says cat, but I've used nano a LOT) and got the password for the next stage.

Password: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

#### Level 1 → Level 2
Logged in with the username `bandit1` and the aforementioned password.

Again, used `ls` to list the files. There was just one file, named `-`. Having dealth with special character files in the past (_yarrrr_, if you know, you know), I went for ```cat <-``` and that give me a string of characters, i.e., the password for the next level.

Password: `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`

#### Level 2 → Level 3
Logged in with the username `bandit2` and the aforementioned password.

`ls` once again. And this time, the file was named `spaces in this filename`. Having experience with such file names (since I, much to the dismay of my friends, name files this way quite often), I went for ```nano "spaces in this filename"``` and duly got the password for the next level.

Password: `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`

#### Level 3 → Level 4
Logged in with the username `bandit3` and the aforementioned password.

Ran `ls`. Got a single folder (yes, _not_ a file this time around) and `cd`'d into it. Ran `ls`, and didn't have any useable files. So, decided to run `ls -a` to expose hidden files, which showed me a `.hidden` file, which I could use ```cat .hidden``` with to extract the contents enclosed.

Password: `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`

#### Level 4 → Level 5
Logged in with the username `bandit4` and the aforementioned password.

Ran `ls`. `cd`'d into the `inhere` folder. Hit a roadblock. Couldn't get anything relevant with `cd`, `nano` or `cat` for the first few files. Yes, I could _probably_ use a script to do this, but it was just 9 files, so I decided to be lazy and just brute force my way through them and got it in the `-file07` file.

Password: `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`

#### Level 5 → Level 6
Logged in with the username `bandit5` and the aforementioned password.

Ran `ls`. Ran `cd inhere` since that was the only folder listed. Running `ls` showed a long list if `maybehereXX` folders, with each containing multiple files. That's a lot of files.

Reading the Bandit documentation told me that the file is **human-readable, 1033 bytes in size and not executable**. Yeah, not worth bruteforcing 19 files. I decided to read up the included documentation and found `find` to be the most relevant, as I could easily use the aforementioned characteristics as argument to help me know which file it is.

Ran ```find -type f -size 1033c ! -executable``` where `-type f` indicates that it's a regular file, `-size 1033c` indicates the 1033 bytes size and `! -executable` indicates that it's not, in fact, executable.

Got the output `./maybehere07/.file2`. Running `cat .file2` gave me the password for the next stage.

Password: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`

#### Level 6 → Level 7
Logged in with the username `bandit6` and the aforementioned password.

Ran `ls`. Got absolutely nothing.  So, they really did mean that the file is stored "somewhere on the server". The given conditions said that the file was **owned by user bandit7, owned by group bandit6, and 33 bytes in size**.

Using the `find` command like before after referring to the documentation, I entered ```find / -user bandit7 -group bandit6 -size 33c```. I used `/` since it looks everywhere across the `root` directory, `-user bandit7` because that is the user who owns it, `-group bandit6` because that is the user who owns it (personally, I feel numbers > names, but hey, I'm lazy00), and `-size 1033c` indicates the size.

Got a lot of errors, so I wanted to get rid of them. Looked it up, and learnt that the errors in Linux/Unix systems are classified under `stderr`, denoted by the number `2`. The relevant command, therefore, is ```find / -user bandit7 -group bandit6 -size 33c 2>/dev/null```, and the relevant line for me was `/var/lib/dpkg/info/bandit7.password`, which helped me get the password using `cat /var/lib/dpkg/info/bandit7.password`.

Password: `z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`

#### Level 7 → Level 8
Logged in with the username `bandit7` and the aforementioned password.

Ran `ls`. It only showed `data.txt` in the directory. Ran `cat data.txt` and got a _really_ long result, long enough that it'd take quite a while to get through, especially since it wasn't alphabetical and I couldn't just scroll to `millionth` . I read up the documentation linked in the [corresponding OverTheWire page](https://overthewire.org/wargames/bandit/bandit8.html) and decided that `grep` would be most convenient to find the relevant line.

I ran ```cat data.txt | grep millionth``` and got just that line as the output. `millionth TESKZC0XvTetK0S9xNwm25STk5iWrBvP`.

Password: `TESKZC0XvTetK0S9xNwm25STk5iWrBvP`

#### Level 8 → Level 9
Logged in with the username `bandit8` and the aforementioned password.

Ran `ls`. Again, just `data.txt`. The problem statement says that the password is in "the only line of text that occurs only once". So, a _unique_ line.

Leafing through the required documentation, I decided to use `sort` to sort the lines alphabetically (thus bringing the duplicates next to each other" and `uniq` to find the unique one.

Running ```sort data.txt | uniq -u``` gave me the required password.

Password: `EN632PlfYiZbn3PhVK3XOGSlNInNE00t`

#### Level 9 → Level 10
Logged in with the username `bandit9` and the aforementioned password.

Ran `ls`. Just `data.txt` again. (We're almost friends now). Anyways, the clue said that the password was in one of the few human-readable strings, preceded by several ‘=’ characters.

That means that the file contains non-human readable data (binary) as well, and I just need the `strings` starting with `=`, which I can find the `grep`.

So, the command was ```cat data.txt | strings | grep ^=```. 

The output was
```yaml
=2""L(
========== passwordk^
========== is
=Y!m
========== G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s
=r=_
=uea
```
which gave me the required password.

Password: `G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s`

#### Level 10 → Level 11
Logged in with the username `bandit10` and the aforementioned password.

Ran `ls`. Got `data.txt` again. The clue says that it contains base64 encoded data, which I could decode using ```cat data.txt | base64 --decode```.

The output was `The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`.

Password: `6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`

#### Level 11 → Level 12
Logged in with the username `bandit11` and the aforementioned password.

Ran `ls`. Got `data.txt` again. Running `cat data.txt` gave me `Gur cnffjbeq vf WIAOOSFzMjXXBC0KoSKBbJ8puQm5lIEi`. The problem statement mentioned that `all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions`, i.e., they've been encoded using the ROT-13 algorithm, something I had fun learning about during my first CTF.

I read up documentation on the `tr` (translate) command and used it to write a command that would apply a ROT-13 decode, with the command being ```cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'```. 

Here `[A-Za-z]` indicates the first set, which includes all the uppercase and lowercase alphabet. `[N-ZA-Mn-za-m]` indicates the second set, which indicates that anything from N-Z maps to a corresponding letter from A-M (and the same happens for lowercase letters.

The decoded output was `The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`.

Password: `JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`

#### Level 12 → Level 13
Logged in with the username `bandit12` and the aforementioned password.

Ran `ls.` Got a hex dump. The guide recommended making a folder in `/tmp`, which I did, using `mkdir /tmp/sherlock`, and tried to move `data.txt` to the folder using `mv data.txt /tmp/sherlock`, and I realised that I couldn't move it, just _copy_ it, so I ended up using `cp data.txt /tmp/sherlock`. I then `cd`'d into it using `cd /tmp/sherlock`.

Using `xxd`'s inbuilt decoder, I tried `xxd -r data.txt`, and got a weird file, which according to the problem statement, is a file that is compressed multiple times.

```
h44�z��A����@=�h4hh��4�i��1������hd��������9���1����������;,�
�����2�3d*58�~  �S�ZP^��luY��Br$�FP!%�s��h�?�)[=�h��O(B��2A���)�tZc��:�pã)�A�ˈ�0���΅A�yjeϢx,�(����z�E�+"�2�/�-��e"���^����t�j���$�d�@�dJơ'7\���$��m1c��#>�aԽ�EV��F��OCӐc@M�C���]��Y2^h8���D=��~  O�I��NDpF�+�|b#Jv�#�J��d�LފW$�Û�͖y�`
                                                           �\&  ��[�@*w�M�0θ��nr��C��`e$b�
     ~�{���
           ��`�<����a��?e:T���e�T4±b����)
                                         �@ِ���x=
```

I had to look up how to save this to a file, which I then did with `xxd -r data.txt > target`. Then, I used the `file` command (as suggested by the problem page) to get the details of the file.

It told me that the file was `gzip compressed data, was "data2.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 573`.

I decided to change the extension using the mv command, `mv target target.gz`. Then, I decoded it with `gunzip target.gz` (after looking up how I can decode gzip files using the CLI. Using `ls`, I saw that another `target` file replaced the previous.

Then, I tried to view it, getting another weirdly encoded file. Running `file target` again. It said that the file was a `target: bzip2 compressed data, block size = 900k`.

Now, since this was a recurring set of events, I'm just going to list commands and results from now on.

Ran `mv target target.bz2`. Then, ran `bzip2 -d target.bz2`. Ran `ls` -> Saw `target` -> `cat target` -> Weirdly encoded file -> `file target` -> `target: gzip compressed data, was "data4.bin", last modified: Thu Oct  5 06:19:20 2023, max compression, from Unix, original size modulo 2^32 20480`

Ran `mv target target.gz`. Then, ran `gunzip target.gz`. Ran `ls` -> Saw `target` -> `cat target` -> Weirdly encoded file -> `file target` -> `target: POSIX tar archive (GNU)`.

Ran `mv target target.tar`. Then, ran `tar -xf target.tar`. Ran `ls` -> Saw `data5.bin` -> `cat data5.bin` -> Weirdly encoded file -> `file data5.bin` -> `target: POSIX tar archive (GNU)`.

Ran `mv data5.bin data5.tar`. Then, ran `tar -xf data5.tar`. Ran `ls` -> Saw `data6.bin` -> `cat data6.bin` -> Weirdly encoded file -> `file data6.bin` -> `data6.bin: bzip2 compressed data, block size = 900k`.

Ran `mv data6.bin data6.bz2`. Then, ran `bzip2 -d data6.bz2`. Ran `ls` -> Saw `data6` -> `file data6` -> `target: POSIX tar archive (GNU)`.

Ran `mv data6 data6.tar`. Then, ran `tar -xf data6.tar`. Ran `ls` -> Saw `data8.bin` -> `file data8.bin` -> `data8.bin: gzip compressed data, was "data9.bin"`.

Ran `mv data8.bin data8.gz`. Then, ran `gunzip data8.gz`. Ran `ls` -> Saw `data8` -> `file data8` -> `data8: ASCII text`.

Now that we finally reached ASCII text, I ran `cat data8` to get `The password is wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw`.

Password: `wbWdlBxEir4CaE8LaPhauuOo6pwRmrDw`

#### Level 13 → Level 14
Logged in with the username `bandit13` and the aforementioned password.

This level, as instructed, didn't have a password stored anyway, just a `sshkey.private` file in the home directory which we could use to connect to the next level using cat, and which I then entered in my SSH client.

SSH Key:
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----
```

Now, since SSH clients are frowned upon, I used `ssh -i sshkey.private bandit14@localhost` since it's on the same host anyhow.

#### Level 14 → Level 15

Logged in via SSH, and was greeted by an elaborate welcome message, the highlight of which was `* PASSWORDS for each level are stored in /etc/somegame_pass/.` Peeking into `/etc/bandit_pass/` using `ls` by following this clue gave me the list of all files that contained passwords for their respective levels and I used `cat bandit14` to print the required password - `fGrHPx402xGC7U7rXKDaxiWFTOiF0ENq`.

The hint requires us to **submit** the password of bandit14 to localhost:3000, which can be done using netcat (which I've used to test server connectivity), so I used `nc localhost 30000` and then pasted the aforementioned password. It states that I am, in fact, `Correct!`, and gave me the password for the next level.

Password: `jN2kgmIXJ6fShzhT2avhotn4Zcka6tnt`.

#### Level 15 → Level 16
Logged in with the username `bandit15` and the aforementioned password.

This level was of a similar format, but required SSL encryption. I looked up any OpenSSL related SSL/TLS clients, and found `openssl s_client`, which I then used to enter `openssl s_client -connect localhost:30001`. I put in the aforementioned password, and got a new one.

Password: `JQttfApK4SeyHwDlI9SXGR50qclOAil1`

#### Level 16 → Level 17
Logged in with the username `bandit16` and the aforementioned password.

In this level, we needed to perform a portscan, so I looked up CLI portscanning tools, and I found `nmap`. Used `nmap localhost -p 31000-32000` to list the number of active listening ports, and got the following output

```
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00039s latency).
Not shown: 996 closed ports
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```
Used the command from the previous level with every port, and for port `31790`, it gave me an RSA key, which I used to log in to the next level.

```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```
#### Level 17 - Level 18

Logged into `bandit17` via the aforementioned key.

The question statement on the website is pretty clear; so I ran the command diff `passwords.new passwords.old`, to get the following output

```
42c42
< hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg
---
> p6ggwdNHncnmCNxuAt0KtKVq185ZU7AW
```

The first password worked and I was immediately kicked out as was mentioned earlier.

Password: `hga5tuuCLF6fFzUpnagiMN8ssu9LFrdg`
_
