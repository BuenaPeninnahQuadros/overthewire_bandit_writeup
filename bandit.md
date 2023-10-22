# Writeup on https://overthewire.org/wargames/bandit/

### Level 0

ssh bandit0@bandit.labs.overthewire.org -p 2220

### Level 0 to Level 1
cat command concatenates files and prints the standard output
'''
cat readme
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/f726d622-6d32-4879-8edf-2d950685b01c)

### Level 1 to Level 2

'''
cat ./-
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/809b92a7-4b5d-49b7-8295-85b0f21add4a)

### Level 2 to Level 3

'''
cat "spaces in this filename"
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/16f60bfa-66dd-44a7-8237-9eff57bc1cf1)

### Level 3 to Level 4

ls -a is the command to list all files/folders
find is the command to search all files in a diectory
'''
ls -a
find .
cat ./inhere/.hidden
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/b305d1cc-d11c-498c-be64-6d4af6483905)

### Level 4 to Level 5

'''
find .
cat ./inhere/-file07
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/c950744c-47c1-4f94-8f98-ac74fb4b971e)

### Level 5 to Level 6

The file was under the inhere diectory and was not executable.
'''
find \! -executable
cat ./inhere/maybehere07/.file2
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/6e08f37c-0526-4755-9c85-33541f861ba3)

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/da1307c2-10ed-4dd2-9ea9-cd4ec17846bf)


### Level 6 to Level 7

The important properties mentioned were : owned by user bandit7, owned by group bandit6, 33 bytes in size
I knew, find command had to be used and I have been informed about the user and the group alongwith the size.
So combining these alongwith the respective flags became my solution. I discovered that 2>/dev/null hid all error messages.
'''
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat var/lib/dpkg/info/bandit7.password
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/9796d854-b799-4ced-899e-1e49892f6f53)


### Level 7 to Level 8

grep command can print lines that match patterns
'''
cat data.txt | grep millionth
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/d0e81ff1-3035-480c-92f1-2f40b6687aff)

### Level 8 to Level 9

This level introduced me to 2 commands- sort and uniq
The prase occurs only once gave me an idea that uniq command has to be used. To bring my files in order so as to find the unique one, sort command had to be used.
'''
sort data.txt | uniq -u
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/5938ec05-cd67-4be8-9df9-a35550bc8be2)

### Level 9 to Level 10

strings command looks for printable strings in a file.
'''
strings data.txt | grep =
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/ce1c1eda-f323-4d49-aeed-526a5dc4a1d8)

### Level 10 to Level 11

My first attempt was to give the command strings data.txt | base64. The output was not the password.
The base64 command can encode binary strings into text representations using the base64 encoding format.
I learnt that -d flag changes ls not to list the files within the specified directory, but to list the information about the directory itself.
'''
base64 -d data.txt
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/40d7a25f-c297-446e-ae86-f47ce93975eb)

### Level 11 to Level 12

https://en.wikipedia.org/wiki/Rot13 provided me with the information.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/8b2c2628-d7fc-49c4-8cc1-95b10845ff53)

'''
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/99834af0-7b17-4e4a-82e2-5521c1bddc68)

### Level 12 to Level 13

The command cd changes the current directory. The command cp copies files and directories.






























