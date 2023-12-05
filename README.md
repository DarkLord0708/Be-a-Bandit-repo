# Be-a-Bandit-repo
## lvl-0:***
<br><br>
    command for establishing connection for level 0<br>
    ```ssh bandit0@bandit.labs.overthewire.org -p 2220```<br>
       password was bandit0<br>
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
    
