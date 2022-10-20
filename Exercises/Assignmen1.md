# Solution to Assignment for Lecture 1

## Question 1

Take away:
* how to check the running Shell: `echo $Shell`

## Question 2

`mkdir` does not support create directories recursively. In this case, we have to first create the `tmp` directory and then create the sub-directory `missing`

**Solution**

```batch
mkdir tmp && mkdir tmp/missing
```

## Question 3

Take away:
* ``touch`` can be used to create an empty file

**Solution**
```batch
touch file.md
touch file.md file1.md file2.md
touch -a file.md
touch --d="next Monday" file.md
```
If you are looking for some examples, you can refer to this page: https://www.geeksforgeeks.org/touch-command-in-linux-with-examples/


## Question 4

**Solution**
```batch
mkdir missing && cd missing
touch semester
```

## Question 5

**Solution**
```batch
mkdir missing && cd missing
touch semester
echo '#!/bin/sh' > semester 
echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
```
Take away:
* Single Quotes can be used to preserve the literal value of the character within the qutoes


## Question 6

**Solution**
```batch
ls -l ./semester
-rw-r--r-- 1  xx xx 61 Oct 20 20:57 semester
```
By checking the permission bits of ``semester`` file, it is not allowed to be executed as the `x` permission bit is missing.

## Question 7

**Solution**
```batch
HTTP/2 200
server: GitHub.com
content-type: text/html; charset=utf-8
last-modified: Sat, 17 Sep 2022 10:59:54 GMT
access-control-allow-origin: *
etag: "6325a8aa-1f37"
expires: Thu, 20 Oct 2022 19:09:20 GMT
cache-control: max-age=600
x-proxy-cache: MISS
x-github-request-id: 081C:F6E8:8E34BB:9280A0:63519A88
accept-ranges: bytes
date: Thu, 20 Oct 2022 19:06:24 GMT
via: 1.1 varnish
age: 424
x-served-by: cache-osl6532-OSL
x-cache: HIT
x-cache-hits: 1
x-timer: S1666292784.373069,VS0,VE2
vary: Accept-Encoding
x-fastly-request-id: 06112476e268c562008353977dc5055863f1e530
content-length: 7991
```
``./semester`` directly lets the `Shell` execute the file as an executable, which is not allowed. However, `sh ./semester` tells the `Shell` to first run the `sh` program, and `./semester` acts the parameter for this program. Then `sh` opens (I think...) this file and interpretes all. Obviously, `./semester` does not need the execute permission bit, as long as it can be accessed and `sh` is allowed to be executed (of course, it can...)

## Question 8
Take away:
* `chmod` is used to change the permission bits for user/group/other/all (there is good reference: https://www.geeksforgeeks.org/chmod-command-linux/)
```batch
# Change file permissions of FOO to be world readable
# and user writable, with no other permissions.

chmod 644 foo
chmod a=r,u+w foo

# Add user and group execute permissions to FOO.

chmod +110 file
chmod ug+x file

# Set file permissions of DIR and subsidiary files to
# be the umask default, assuming execute permissions for
# directories and for files already executable.
# -R denotes for recursively, while `,` (to my understanding...) denotes for each file in the directory.

chmod -R a=,+rwX dir
```

## Question 9
**Solution**
```batch
# Only give the execute permission to the user 
chmod u+x semester
```
Take away (https://en.wikipedia.org/wiki/Shebang_(Unix)):
* Shebang: `#!` special character sequence used at the beginning of a script. 
* All contents after the `#!` are parsed as an interpreter directive. For example, in [Question 5](#question-5), `'#!/bin/sh'` are refering to the `sh` interpreter. The parameter passed to the interpreter is the path of the script. However, the `Shebang` could be ignored by the interpreter as `#` is a comment marker in some scripting languages.
```batch
# More examples taken from wiki

#!/usr/bin/env python3
#!/bin/bash
```

## Question 10
**Solution**
```batch
./semester | grep --ignore-case last-modified > ~/last-modified.txt
```

Take away:
* ``grep`` (global regular expression search), which is used to search a file for a particular pattern of characters. (https://www.geeksforgeeks.org/grep-command-in-unixlinux/)


## Question 11
**Solution**
```batch
cat /sys/class/power/sypply/BAT0/capacity
```
NOTE: When I tried to check the status of the battery in my laptop with Ubuntu 22.04 installed, the output is `Unknown`. It seems that there could be some issue of the driver/sensor. Besides, I did not find any information related to CPU temperature in the WSL2 on my desktop. I will update this question later once I figured the issues out.