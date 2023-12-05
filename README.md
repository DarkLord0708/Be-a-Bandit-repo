# Be-a-Bandit-repo
<u>lvl-0:</u>
    command for establishing connection for level 0
    ```ssh bandit0@bandit.labs.overthewire.org -p 2220```
       password was bandit0
    used ```ls``` to see all the files in the directory
    found readme, used ```cat readme``` and found the password for the next leevl

<u>lvl-1:</u>
    established connection for level 1
    can't directly cat a file with name starting with '-'
    so, used ```cat ./-```, found the next password


(I'll only list significant commands further on )
<u>lvl-2:</u>
    ```cat 'spaces in this filename'```

<u>lvl-3:</u>
    ```cd inhere
       find
       cat ./.hidden```

<u>lvl-4:</u>
    ```cd inhere
       ls
       find -readable
       cat ./-file07```

<u>lvl-5:</u>
    ```cd inhere
       ls
       find -readable -size 1033c ! -executable```
       from this got, maybehere07/file2

<u>lvl-6:</u>
    ```ls -a``` but got nothing from here
    ```find / -user bandit7 -group bandit6 -size 33c``` got a list of many files, most of them had access denied and some didn't exist but one file didn't have denied access, it was ```/var/lib/dpkg/info/bandit7.password```
    then used cat for that file
    
