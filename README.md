# Be-a-Bandit-repo (all the passwords are stored in passwords.txt)
## lvl-0:
<br><br>
    command for establishing connection for level 0<br>
    ```ssh bandit0@bandit.labs.overthewire.org -p 2220```<br>
       password was `bandit0`<br>
    used ```ls``` to see all the files in the directory<br>
    found readme, used ```cat readme``` and found the password for the next level<br>
<br>
## lvl-1:
<br><br>
    established connection for level 1<br>
    can't directly cat a file with name starting with '-'<br>
    so, used ```cat ./-```, found the next password<br>

<br>
(I'll only list significant commands further on )<br><br>

## lvl-2:
<br><br>
    ```cat 'spaces in this filename' ```<br>
<br>
## lvl-3:
<br><br>
    ``` cd inhere ```<br>
    `` find ``<br>
    `` cat ./.hidden ``<br>
<br>
## lvl-4:
<br><br>
    ```cd inhere<br>
       ls<br>
       find -readable<br>
       cat ./-file07```<br>
<br>
## lvl-5:
<br><br>
    ```cd inhere<br>
       ls<br>
       find -readable -size 1033c ! -executable```<br>
       from this got, maybehere07/file2<br>
<br>
## lvl-6:
<br><br>
    ```ls -a``` but got nothing from here<br>
    ```find / -user bandit7 -group bandit6 -size 33c``` got a list of many files, most of them had access denied and some didn't exist but one file didn't have denied access, it was ```/var/lib/dpkg/info/bandit7.password```<br>
    then used cat for that file<br>
<br>
## lvl-7:
<br><br>
```man grep```<br>
```grep 'millionth' data.txt```<br>
this gave the password<br>
<br>
## lvl-8:
<br><br>
```sort data.txt | uniq -u```<br>
this gave the password<br>
<br>
## lvl-9:
<br><br>
```strings data.txt | grep '=='```<br>
this gave the password<br>
<br>
## lvl-10:
<br><br>
had to decode a base64 encoded file, sor used:<br>
```base64 -d data.txt```<br>
this gave the password<br>
<br>
## lvl-11:
<br><br>
had to translate data using ```tr``` because the alphabets were rotated by 13 values and this could be decoded by<br>
```cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'```<br>
this gave the password<br>
<br>
## lvl-12:
<br><br>
file was encrypted multiple times and I didn't have permission to read in the home directory so, I made a temporary directory using,<br>
```mkdir /tmp/darklord```<br>
and then sent the file's decoded contents to the new directory using,<br>
```cat data.txt | xxd -r > /tmp/darklord/data1```<br>
then I changed directories<br>
```cd /tmp/darklord```<br>
to see the type of file, I used,<br>
```file data1```<br>
found out that it was a gzip encoded file, then used<br>
```zcat data1 > data2```<br>
then I used,<br>
```file data2``` and found that this one was a bzip2 encoded file, then used<br>
```bzcat data2 > data3```<br>
and then repeated the same task, using the following commands<br>
```file data3``` this was a gzip file<br>
```zcat data3 > data4```<br>
```file data4``` this was a tar archive file<br>
I had to extract this archive, did so using ```tar -xvf data4``` this gave a data5.bin<br>
continuing,<br>
```file data4.bin``` this was a tar archive aswell<br>
```tar -xvf data5.bin``` this gave a data6.bin<br>
```file data6.bin``` this was a bzip2 file<br>
```bzcat data6.bin > data7```<br>
```file data7``` this was a tar archive<br>
```tar -xvf data7``` this gave data8.bin<br>
```file data8.bin``` this was a gzip file<br>
```zcat data8.bin > data9```<br>
```file data9``` this was an ASCII text file<br>
```cat data9``` gave the password<br>
<br>
## lvl-13:
<br><br>
there was no password but we had a ssh key in sshkey.private copied its contents to a file on my desktop.<br>
Using google I found that I can use ```-i``` tag to use an identity file but this said that the file was too open.<br>
So we had to limit its permissions. Read some about ```chmod``` and used,<br>
```chmod 700 private.key``` here private.key was the file on my desktop ,then I used<br>
```ssh -i ./Desktop/private.key bandit14@bandit.labs.overthewire.org -p 2220```<br>
and we got in the next level<br>
there I found the password from<br>
```cat /etc/bandit_pass/bandit14```<br>
<br>
## lvl-14:
<br><br>
had to use net cat<br>
```nc localhost 30000```<br>
entered the password of level 14 when prompted<br>
this gave the password<br>
<br>
## lvl-15:
<br><br>
read some more about openssl and s_client and used,<br>
```openssl s_client -connect localhost:30001```<br>
entered the password of the current level when prompted and this gave the password<br>
<br>
## lvl-16:
<br><br>
for posrt scanning, used nmap<br>
```nmap localhost -p 31000-32000```<br>
got four ports:<br>
31046, 31518, 31691, 31790, 31960<br>
all these were open, tcp, unknown service<br>
for getting all the info about these ports,<br>
```nmap localhost -p 31046,31518,31691,31790,31960 -A```<br>
took sometime but got<br>
31046 had echo<br>
31518 had ssl/echo <br>
31691 had echo<br>
31790 has ssl/unknown <br>
31960 had echo<br>
as far as I know, ```echo``` shows the same info back, So I used 31790<br>
got an ssh key and stored it in a file on Desktop.<br>
<br>
## lvl-17:
<br><br>
used ssh key to login, after changing the permissions, and got in<br>
had to use diff,<br>
```diff passwords.new passwords.old```<br>
output had two passwords, one with > and other with <.<br>
'>' showed the old one because old file was given on the right side and '<' showed new one<br>
<br>
## lvl-18:
<br><br>
was getting logged out as soon as I was loggin in,<br>
checked ```man ssh``` and found out that I can pass commands with ssh, so did<br>
```ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme``` because I knew that the password was in readme<br>
this gave the password<br>
<br>
## lvl-19:
<br><br>
found a setuid binary file, used<br>
```./bandit20-do```<br>
found that I became bandit20 user as long as I use ```./bandit20-do``` before any commands I use, hence passsword was found using,<br>
```./bandit20-do cat /etc/bandit_pass/bandit20```<br>
<br>
## lvl-20:
<br><br>
### process:
using net cat setup a listening connection to some port on localhost.<br>
Now using ```suconnect``` connect to the same port and once the connection is established,<br>
send the passsword from the netcat terminal and as the password matches, we will get the correct password back<br>
#### Terminal_1:
```nc -lp 9000```(can use any port, I used this because loewr ports were in use)<br>
#### Terminal_2:
```./suconnect 9000```<br>
#### Terminal_1:
entered the password of lvl20<br>
#### Terminal_2:
accepts<br>
#### Terminal_1:
gives out the password of lvl21<br>
<br>
## lvl-21:
<br><br>
```cd /etc/cron.d```<br>
```cat cronjob_bandit22``` (Because it was the next lvl and it only made sense)<br>
this gave an address to a shell file, used<br>
```cat /usr/bin/cronjob_bandit22.sh```<br>
got the inputs and saw that a file had read permissions and was storing the password, used<br>
```cat``` and got the password<br>
<br>
## lvl-22:
<br><br>
like lvl21, opened cronjob.bandit23, went to the specified address and found a script<br>
it was entering the passwords in ```/tmp/username``` where username was the username of the user<br>
```tmp/$mytarget``` here mytarget can be found by using the script that's running,<br>
just copy and run it to get %mytarget and then just ```cat /tmp/[the found target]```<br>
and hence got the password<br>
<br>
## lvl-23:
<br><br>
found the cronjob and saw that it was deleting all the files in a directory after executing them<br>
we can get the password if the script<br>
```cat /etc/bandit_pass/bandit24``` is run<br>
so I wrote a small script<br>
```#!/bin/bash```<br>
```cat /etc/bandit_pass/bandit24 > /tmp/darklord/pass.txt```<br>
/tmp/darklord was a temporary directory I made to work on by<br>
```mkdir /tmp/darklord```<br>
I used ```nano``` to make the script and named the script "haha.sh"<br>
so I cpoied this script file in the directory in which the cronjob was working used,<br>
```cp haha.sh /var/spool/bandit24/foo/```<br>
and after about 2 minutes I got pass.txt and it contained the password<br>
<br>
## lvl-24:
<br><br>
have to enetr password + " " + a four digit pin to a daemon listining at port 30002<br>
```nc localhost 30002```<br>
now as we don't know the pin and as the question suggests, we have to brute force it.<br>
On wrong input we get the message "Wrong! Please enter the correct pincode. Try again."<br>
and it doesn't log us out, which is good<br>
I wrote a small script (cracker.sh)<br>
```#!/bin/bash```<br>
```for i in {0..9}{0..9}{0..9}{0..9}```<br>
```do```<br>
```    echo "password_of_lvl $i" >> list.txt```<br>
```done```<br>
then did,<br>
```chmod +x cracker.sh```<br>
doing ```./cracker.sh``` created list.txt<br>
then I piped the contents of list.txt in the daemon by<br>
```cat list.txt | nc localhost 30002```<br>
But piping the whole list wasn't working because my terminal kept hanging midway and I was not sure it was not working or<br>
taking some extra time. So, I separated list.txt into 5 lists and then piped them one by one<br>
the password was found in list5.txt and after a bit of poking around, I found that the pincode was 9015<br>
<br>
## lvl-25:
<br><br>
found an ssh key and used the usual was by applying ```-i``` tag in ssh but it doesn't work.<br>
The usual message does load up but connection gets closed.<br>
Also the question suggests that that this user is not running on ```/bin/bash```<br>
then as user bandit25, used,<br>
```cat /etc/passwd | grep bandit26```<br>
found that its running ```/bin/showtext```<br>
to see what it is,<br>
```cat /usr/bin/showtext```<br>
found it was a bash script, this conatins "more" and more is used while displaying larger texts so that it fits<br>
the screen, like man pages, also doing ```man more``` I got to know that it can take commands via ![command]<br>
But this wasn't working, bit of googling helped me to get introduced to "vi", this makes a new editor which<br>
can be used to run commands. Now, in vi you can run commands by launching a shell via<br>
```:shell```<br>
but this doesn't help because its launching the same shell. To check the shell use<br>
```:set shell?``` gave shell = /usr/bin/showtext<br>
to change shell we can use<br>
```:set shell = /usr/bin/bash``` to set shell to /bin/bash<br>
so now we use ```:shell``` and we enter our bash shell again<br>
and ```cat /etc/bandit_pass/bandit26``` will give the passowrd<br>
<br>
## lvl-26:
<br><br>
as we're already in the shell we see "bandit27-do" in the directory, we've seen a similar program<br>
this will run commands as bandit27, so I used,<br>
```./bandit27-do cat /etc/bandit_pass/bandit27```<br>
and this gave the password<br>
<br>
## lvl-27:
<br><br>
had to use git clone but at a certain port for the specified ssh url, specifying the port was something I had<br>
to google. I used,<br>
```git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo```
and entered the pass of lvl 27 when prompted, this created a repository ion the directory I was working on<br>
which was /tmp/darklord2<br>
```ls -l repo```<br>
gave that it had a README file<br>
```cat /repo/README```<br>
gave the password<br>
<br>
## lvl-28:
<br><br>
repeated the same steps as lvl27 and got to the cloned repo, this time it had a README.md file<br>
its contents had password hidden, used,<br>
```git log``` and found out that there were 3 commits,<br>
```git checkout <the hash of the commit>```<br>
the second commit caintained the password<br>
<br>
## lvl-29:
<br><br>
repeated all the steps as lvl 28, this time password was not in produciton in the README file<br>
so to check other branches I used,<br>
```git branch -a```<br>
as we were already on origin/master branch so, checked /origin/dev using,<br>
```git checkout remotes/origin/dev```<br>
this gave the password<br>
<br>
## lvl-30:
<br><br>
repeated the same steps as lvl 29 but this time, there were no other branches and README file was empty<br>
So I used,<br>
```git tag```<br>
so there was a tag called "secret", I used<br>
```git show secret```<br>
this gave the password<br>
<br>
## lvl-31:
<br><br>
same as the last time but this time README.md says that the test is to push a file "key.txt"<br>
and the contents of key.txt were given. So I created the key.txt file and entered its contents using,<br>
```nano key.txt``` and added the required content, then used<br>
```git add -f key.txt```<br>
```git commit``` wrote a commit message<br>
```git push```<br>
this gave us the next password<br>
<br>
## lvl-32:
<br><br>
some new shell appeared, this was returning every command that user enetered in uppercase, it looked like<br>
```sh: 1: <command in uppercase>```<br>
deciphering it was a bit troublesome, had to google a lot but then I came across positional parameter "$0"<br>
and using ```$0``` allowed me to enter "sh:" shell, doing ```whoami``` gave bandit33<br>
so I found password using,<br>
```cat /etc/bandit_pss/bandit33```<br>
<br>
## lvl-33:
<br><br>
was the last level and only had a readme.txt file which said congratulations.
