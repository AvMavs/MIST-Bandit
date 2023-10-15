# Bandit - The Writeup

#### Level 0
Well, yes, one _should_ in theory prefer a linux terminal for this. But the convenience of a GUI client is quite nice, so I used Termius, something I already use for the rest of my SSH and SFTP needs. The [website for Bandit](https://overthewire.org/wargames/bandit/bandit0.html) provides the user credentials required.

![image](https://github.com/AvMavs/Cryptonite-Bandit/assets/82929505/8a470182-20f9-48b5-97ec-1796748a5e1d)


#### Level 0 → Level 1
I used the command `ls` to list the files in the default home directory that we log in to. It only shows one file, a `readme`. I thought it was a folder and tried `cd`-ing into it, but... _yeah._ Then I went for `nano readme` (I know, I know, the guide says cat, but I've used nano a LOT) and got the password for the next stage.

Password: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

#### Level 1 → Level 2
Logged in with the username `bandit1` and the aforementioned password.

Again, used `ls` to list the files. There was just one file, named `-`. Having dealth with special character files today (_yarrrr_, if you know, you know), I went for `cat <-` and that give me a string of characters, i.e., the password for the next level.

Password: `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`

#### Level 2 → Level 3
Logged in with the username `bandit2` and the aforementioned password.

`ls` once again. And this time, the file was named `spaces in this filename`. 
