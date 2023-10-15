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
Logged in with the username `bandit4` and the aforementioned password.

Ran `ls`. Ran `cd inhere` since that was the only folder listed. Running `ls` showed a long list if `maybehereXX` folders, with each containing multiple files. That's a lot of files.

Reading the Bandit documentation told me that the file is **human-readable, 1033 bytes in size and not executable**. Yeah, not worth bruteforcing 19 files. I decided to read up the included documentation and found `find` to be the most relevant, as I could easily use the aforementioned characteristics as argument to help me know which file it is.

Ran `find -type f -size 1033c ! -executable` where `-type f` indicates that it's a regular file, `-size 1033c` indicates the 1033 bytes size and `! -executable` indicates that it's not, in fact, executable.

Got the output `./maybehere07/.file2`. Running `cat .file2` gave me the password for the next stage.

Password: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`






