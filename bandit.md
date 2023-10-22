# Writeup on https://overthewire.org/wargames/bandit/

### Level 0

ssh bandit0@bandit.labs.overthewire.org -p 2220

### Level 0 to Level 1
cat command concatenates files and prints the standard output
'''
cat readme
'''

### Level 1 to Level 2

'''
cat ./-
'''

### Level 2 to Level 3

'''
cat "spaces in this filename"
'''

### Level 3 to Level 4

ls -a is the command to list all files/folders
find is the command to search all files in a diectory
'''
ls -a
find .
cat ./inhere/.hidden
'''
### Level 4 to Level 5

'''
find .
cat ./inhere/-file07
'''

### Level 5 to Level 6

The file was under the inhere diectory and was not executable.
'''
find \! -executable
cat ./inhere/maybehere07/.file2
'''

### Level 6 to Level 7

The important properties mentioned were : owned by user bandit7, owned by group bandit6, 33 bytes in size
I knew, find command had to be used and I have been informed about the user and the group alongwith the size.
So combining these alongwith the respective flags became my solution. I discovered that 2>/dev/null hid all error messages.
'''
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat var/lib/dpkg/info/bandit7.password
'''

### Level 7 to Level 8

grep command can print lines that match patterns
'''
cat data.txt | grep millionth
'''

### Level 8 to Level 9

This level introduced me to 2 commands- sort and uniq
The prase occurs only once gave me an idea that uniq command has to be used. To bring my files in order so as to find the unique one, sort command had to be used.
'''
sort data.txt | uniq -u
'''

### Level 9 to Level 10

strings command looks for printable strings in a file.
'''
strings data.txt | grep =
'''

### Level 10 to Level 11

My first attempt was to give the command strings data.txt | base64. The output was not the password.
The base64 command can encode binary strings into text representations using the base64 encoding format.
I learnt that -d flag changes ls not to list the files within the specified directory, but to list the information about the directory itself.
'''
base64 -d data.txt
'''

### Level 11 to Level 12

https://en.wikipedia.org/wiki/Rot13 provided me with the information.
'''
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
'''

### Level 12 to Level 13


























