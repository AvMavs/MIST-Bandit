# Bandit - The Writeup

#### Level 0
Well, yes, one _should_ in theory prefer a linux terminal for this. But the convenience of a GUI client is quite nice, so I used Termius, something I already use for the rest of my SSH and SFTP needs. The [website for Bandit](https://overthewire.org/wargames/bandit/bandit0.html) provides the user credentials required.

![image](https://github.com/AvMavs/Cryptonite-Bandit/assets/82929505/8a470182-20f9-48b5-97ec-1796748a5e1d)


#### Level 0 → Level 1
I used the command `ls` to list the files in the default home directory that we log in to. It only shows one file, a `readme`. I thought it was a folder and tried `cd`-ing into it, but... _yeah._ Then I went for `nano readme` (I know, I know, the guide says cat, but I've used nano a LOT) and got the password for the next stage.

Password: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

#### Level 1 → Level 2
Logged in with the username `bandit1` and the aforementioned password.

Again, used `ls` to list the files. There was just one file, named `-`. Having dealth with special character files in the past (_yarrrr_, if you know, you know), I went for `cat <-` and that give me a string of characters, i.e., the password for the next level.

Password: `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`

#### Level 2 → Level 3
Logged in with the username `bandit2` and the aforementioned password.

`ls` once again. And this time, the file was named `spaces in this filename`. Having experience with such file names (since I, much to the dismay of my friends, name files this way quite often), I went for `nano "spaces in this filename"` and duly got the password for the next level.

Password: `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`

#### Level 3 → Level 4
Logged in with the username `bandit3` and the aforementioned password.

Ran `ls`. Got a single folder (yes, _not_ a file this time around) and `cd`'d into it. Ran `ls`, and didn't have any useable files. So, decided to run `ls -a` to expose hidden files, which showed me a `.hidden` file, which I could use `cat .hidden` with to extract the contents enclosed.

Password: `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`

#### Level 4 → Level 5
Logged in with the username `bandit4` and the aforementioned password.

Ran `ls`. `cd`'d into the `inhere` folder. Hit a roadblock. Couldn't get anything relevant with `cd`, `nano` or `cat` for the first few files. Yes, I could _probably_ use a script to do this, but it was just 9 files, so I decided to be lazy and just brute force my way through them and got it in the `-file07` file.

Password: `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`

#### Level 5 → Level 6
Logged in with the username `bandit5` and the aforementioned password.

Ran `ls`. Ran `cd inhere` since that was the only folder listed. Running `ls` showed a long list if `maybehereXX` folders, with each containing multiple files. That's a lot of files.

Reading the Bandit documentation told me that the file is **human-readable, 1033 bytes in size and not executable**. Yeah, not worth bruteforcing 19 files. I decided to read up the included documentation and found `find` to be the most relevant, as I could easily use the aforementioned characteristics as argument to help me know which file it is.

Ran `find -type f -size 1033c ! -executable` where `-type f` indicates that it's a regular file, `-size 1033c` indicates the 1033 bytes size and `! -executable` indicates that it's not, in fact, executable.

Got the output `./maybehere07/.file2`. Running `cat .file2` gave me the password for the next stage.

Password: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`

#### Level 6 → Level 7
Logged in with the username `bandit6` and the aforementioned password.

Ran `ls`. Got absolutely nothing.  So, they really did mean that the file is stored "somewhere on the server". The given conditions said that the file was **owned by user bandit7, owned by group bandit6, and 33 bytes in size**.

Using the `find` command like before after referring to the documentation, I entered `find / -user bandit7 -group bandit6 -size 33c`. I used `/` since it looks everywhere across the `root` directory, `-user bandit7` because that is the user who owns it, `-group bandit6` because that is the user who owns it (personally, I feel numbers > names, but hey, I'm lazy00), and `-size 1033c` indicates the size.

```yaml
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/polkit-1/localauthority’: Permission denied
find: ‘/etc/sudoers.d’: Permission denied
find: ‘/etc/multipath’: Permission denied
find: ‘/root’: Permission denied
find: ‘/boot/efi’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/snapd/cookie’: Permission denied
find: ‘/var/lib/snapd/void’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/chrony’: Permission denied
find: ‘/var/lib/polkit-1’: Permission denied
find: ‘/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/update-notifier/package-data-downloads/partial’: Permission denied
find: ‘/var/lib/amazon’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/log’: Permission denied
find: ‘/var/cache/private’: Permission denied
find: ‘/var/cache/pollinate’: Permission denied
find: ‘/var/cache/apparmor/30d07b40.0’: Permission denied
find: ‘/var/cache/apparmor/a4dd844e.0’: Permission denied
find: ‘/var/cache/apt/archives/partial’: Permission denied
find: ‘/var/cache/ldconfig’: Permission denied
find: ‘/var/tmp’: Permission denied
find: ‘/var/snap/lxd/common/lxd’: Permission denied
find: ‘/var/crash’: Permission denied
find: ‘/sys/kernel/tracing’: Permission denied
find: ‘/sys/kernel/debug’: Permission denied
find: ‘/sys/fs/pstore’: Permission denied
find: ‘/sys/fs/bpf’: Permission denied
find: ‘/proc/tty/driver’: Permission denied
find: ‘/proc/1343004/task/1343004/fd/6’: No such file or directory
find: ‘/proc/1343004/task/1343004/fdinfo/6’: No such file or directory
find: ‘/proc/1343004/fd/5’: No such file or directory
find: ‘/proc/1343004/fdinfo/5’: No such file or directory
find: ‘/home/bandit31-git’: Permission denied
find: ‘/home/drifter8/chroot’: Permission denied
find: ‘/home/drifter6/data’: Permission denied
find: ‘/home/bandit27-git’: Permission denied
find: ‘/home/bandit5/inhere’: Permission denied
find: ‘/home/bandit30-git’: Permission denied
find: ‘/home/bandit29-git’: Permission denied
find: ‘/home/bandit28-git’: Permission denied
find: ‘/home/ubuntu’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/dev/mqueue’: Permission denied
find: ‘/dev/shm’: Permission denied
find: ‘/lost+found’: Permission denied
find: ‘/snap’: Permission denied
find: ‘/drifter/drifter14_src/axTLS’: Permission denied
find: ‘/run/chrony’: Permission denied
find: ‘/run/user/11017’: Permission denied
find: ‘/run/user/11029’: Permission denied
find: ‘/run/user/11030’: Permission denied
find: ‘/run/user/11010’: Permission denied
find: ‘/run/user/11011’: Permission denied
find: ‘/run/user/11019’: Permission denied
find: ‘/run/user/11025’: Permission denied
find: ‘/run/user/11015’: Permission denied
find: ‘/run/user/8004’: Permission denied
find: ‘/run/user/11032’: Permission denied
find: ‘/run/user/11009’: Permission denied
find: ‘/run/user/11007’: Permission denied
find: ‘/run/user/11003’: Permission denied
find: ‘/run/user/11024’: Permission denied
find: ‘/run/user/11023’: Permission denied
find: ‘/run/user/11020’: Permission denied
find: ‘/run/user/11014’: Permission denied
find: ‘/run/user/11002’: Permission denied
find: ‘/run/user/11008’: Permission denied
find: ‘/run/user/11016’: Permission denied
find: ‘/run/user/11004’: Permission denied
find: ‘/run/user/11000’: Permission denied
find: ‘/run/user/11005’: Permission denied
find: ‘/run/user/11013’: Permission denied
find: ‘/run/user/11006/systemd/inaccessible/dir’: Permission denied
find: ‘/run/user/11001’: Permission denied
find: ‘/run/user/11012’: Permission denied
find: ‘/run/sudo’: Permission denied
find: ‘/run/screen/S-bandit20’: Permission denied
find: ‘/run/multipath’: Permission denied
find: ‘/run/cryptsetup’: Permission denied
find: ‘/run/lvm’: Permission denied
find: ‘/run/credentials/systemd-sysusers.service’: Permission denied
find: ‘/run/systemd/propagate’: Permission denied
find: ‘/run/systemd/unit-root’: Permission denied
find: ‘/run/systemd/inaccessible/dir’: Permission denied
find: ‘/run/lock/lvm’: Permission denied
```

The relevant line for me was `/var/lib/dpkg/info/bandit7.password` and I got the password using `cat /var/lib/dpkg/info/bandit7.password`.

Password: `z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`

#### Level 7 → Level 8
Logged in with the username `bandit7` and the aforementioned password.

Ran `ls`. It only showed `data.txt` in the directory. Ran `cat data.txt` and got a _really_ long result, long enough that it'd take quite a while to get through, especially since it wasn't alphabetical and I couldn't just scroll to `millionth` . I read up the documentation linked in the [corresponding OverTheWire page](https://overthewire.org/wargames/bandit/bandit8.html) and decided that `grep` would be most convenient to find the relevant line.

I ran `cat data.txt | grep millionth` and got just that line as the output. `millionth TESKZC0XvTetK0S9xNwm25STk5iWrBvP`.

Password: `TESKZC0XvTetK0S9xNwm25STk5iWrBvP`

#### Level 8 → Level 9
Logged in with the username `bandit8` and the aforementioned password.

Ran `ls`. Again, just `data.txt`. The problem statement says that the password is in "the only line of text that occurs only once". So, a _unique_ line.

Leafing through the required documentation, I decided to use `sort` to sort the lines alphabetically (thus bringing the duplicates next to each other" and `uniq` to find the unique one.

Running `sort data.txt | uniq -u` gave me the required password.

Password: `EN632PlfYiZbn3PhVK3XOGSlNInNE00t`

#### Level 9 → Level 10
Logged in with the username `bandit9` and the aforementioned password.

Ran `ls`. Just `data.txt` again. (We're almost friends now). Anyways, the clue said that the password was in one of the few human-readable strings, preceded by several ‘=’ characters.

That means that the file contains non-human readable data (binary) as well, and I just need the `strings` starting with `=`, which I can find the `grep`.

So, the command was `cat data.txt | strings | grep ^=`. 

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

Ran `ls`. Got `data.txt` again. The clue says that it contains base64 encoded data, which I could decode using `cat data.txt | base64 --decode`.

The output was `The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`.

Password: `6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`

#### Level 11 → Level 12
