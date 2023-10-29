# Writeup on https://overthewire.org/wargames/bandit/

### Level 0

ssh bandit0@bandit.labs.overthewire.org -p 2220

### Level 0 to Level 1
ls is a command to list computer files and directories. On giving the command ls, it displays readme which means a file named readme exists.
cat command concatenates files and prints the standard output. 
'''
cat readme
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/d8c748e7-f9a8-4154-9508-bbd94b45593b)


### Level 1 to Level 2

'''
cat ./-
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/2165f778-919a-4a74-9986-fb25f6d3009b)


### Level 2 to Level 3

'''
cat "spaces in this filename"
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/0ee08c70-6814-4c04-b5b2-758a99592060)


### Level 3 to Level 4

ls -a is the command to list all files/folders <br>
find is the command to search all files in a diectory. <br>
'''
ls -a
find .
cat ./inhere/.hidden
''' <br>
In Unix-like and some other operating systems, find is a command-line utility that locates files based on some user-specified criteria and either prints the pathname of each matched object or, if another action is requested, performs that action on each matched object.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/72e077ce-0b1b-4ee1-9f4a-5e1e1e711c17)


### Level 4 to Level 5

'''
find .
cat ./inhere/-file07
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/54187ad2-b4fa-4852-9048-698edc1c4958)


### Level 5 to Level 6

The file was under the inhere diectory and was not executable.
'''
find \! -executable
cat ./inhere/maybehere07/.file2
'''
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/521c5f2a-e776-4d27-b8ed-cdf4933efb8c)

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/50defa66-515e-4d17-a8ea-e2145ba64a55)



### Level 6 to Level 7

The important properties mentioned were : owned by user bandit7, owned by group bandit6, 33 bytes in size
I knew, find command had to be used and I have been informed about the user and the group alongwith the size.
So combining these alongwith the respective flags became my solution. I discovered that 2>/dev/null hid all error messages.
'''
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat var/lib/dpkg/info/bandit7.password
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/e86c2acd-d1a8-4ddf-80a2-82148fe85b8e)



### Level 7 to Level 8

The grep command can print lines that match patterns.
Pipe operator is used to combine two or more commands.
'''
cat data.txt | grep millionth
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/4b032560-fe9a-4082-89df-1c37c1e95bc5)


### Level 8 to Level 9

This level introduced me to 2 commands- sort and uniq
The prase occurs only once gave me an idea that uniq command has to be used. To bring my files in order so as to find the unique one, sort command had to be used.
'''
sort data.txt | uniq -u
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/f16d464f-537f-4b2c-b1e1-2d5d5afafba1)


### Level 9 to Level 10

strings command looks for printable strings in a file.
'''
strings data.txt | grep =
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/d3c06208-c3dd-4d73-81e8-2df4146c0d7c)

### Level 10 to Level 11

My first attempt was to give the command strings data.txt | base64. The output was not the password.
The base64 command can encode binary strings into text representations using the base64 encoding format.
I learnt that -d flag changes ls not to list the files within the specified directory, but to list the information about the directory itself.
'''
base64 -d data.txt
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/cd935254-cc23-435c-ace8-240192a83a2d)

### Level 11 to Level 12

https://en.wikipedia.org/wiki/Rot13 provided me with the information.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/4ce97adc-b254-458a-8fc6-39705cf63cef)


'''
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
'''

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/f6727feb-d4ec-43dc-b072-939641cdb2cb)


### Level 12 to Level 13

The first step was to create a directory using mkdir command, naming it as buenapq. <br>
'''
mkdir /tmp/buenapq
'''
<br>
The command cp copies files and directories. So I copied the directory I just created.
The command cd changes the current directory. To navigate to the current directory I used the cd command. On listing out the directory, I found that data.txt file exists. <br>
xxd - make a hexdump or do the reverse. This command has to be used to create a hexdump of a file or to reverse the hexdump format to a binary output. In this level the application of xxd is to do the reverse. So the next step was to reverse the data.txt file to data using xxd command. <br>
Next I used the file command to know the file type of data. I got the output as gzip compressed data,was 'data2.bin".
I quickly went through the manual for gzip and understood that, if  the  compressed  file  name is too long for its file system, gzip truncates it.  Gzip attempts to truncate only the parts of the file name longer than 3 characters. The command gzip -d will decompress the file.
Before decompressing the file data, I moved it to another file called file.gz. Then I typed the command ''' gzip -d file.gz ''' to decompress it. 
The file type of file was bzip2 compressed data. <br>
bzip2 - compresses  files  using the Burrows-Wheeler block sorting text compression algorithm, and Huff‐man coding.
I moved the file to file.bz2 and then gave the command ''' bzip2 -d file.bz2 ''' to decompress it. Again on listing out, I saw file in my directory and its file type was again gzip compressed. I moved the file to file.gz and then decompressed it.
Now on seeking the file type on file, it displayed POSIX tar archive(GNU). <br>
I moved the file to file.tar and then used the tar command to extract the file from file.tar.
'''
tar xf file.tar
'''
<br>
On using the ls command, it dispayed data5.bin in the list. I found the filetype of data5.bin to be a tar archive. So after repeating the same process, I got data6.bin file in the list which was bzip2 compressed. After decompressing it, I checked the file type of data which was tar archive.
I moved the file data to data1.tar and then typed ''' tar xf data1.tar '''
The file data8.bin was decompressed and finally the file type of data was ASCII text. <br>
On reading the file data, I got the password.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/6b89da0d-4a87-4c4c-b060-ca9ff3408ae6)
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/ece9c9b6-388f-4fd7-be7c-f4278bf76ab2)

### Level 13 to Level 14

ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine. <br>
 -i identity_file:  Selects a file from which the identity (private key) for public key authentication is read.
 After logging in to bandit14 using the sshkey.private, I read the file /etc/bandit_pass/bandit14 to get the password.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/bc1415aa-8504-4764-a945-e42fa4cd9d15)


![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/e376947c-95de-494b-ae2a-c11898b6dc6c)


### Level 14 to Level 15

 The telnet command is used for interactive communication with another host using the TELNET protocol. To connect to the port 30000 on localhost, the command to be given is ''' telnet localhost 30000 '''
![Screenshot 2023-10-26 235046](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/db00e42f-be53-4a5d-92ac-3dec18165787)

### Level 15 to Level 16

For this level we start by using the openssl s_client command.  This command implements a generic SSL/TLS client which connects to a remote host using SSL/TLS. It is a very useful diagnostic tool for SSL servers.   <br>
'''-connect host:port ''' specifies the host and optional port to connect to.
           
![Screenshot 2023-10-27 204017](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/bf270cff-4125-404d-89be-e1ecb7166ee2)

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/34890f04-884b-42bb-949a-9401def23607)

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/53ea1af8-aeea-4709-ae83-c5697d324ce8)

### Level 16 to Level 17

 Nmap (“Network Mapper”) is an open source tool for network exploration and security auditing. The output from Nmap is a list of scanned targets, with supplemental information on each depending on the options used. <br>
 In this level we need to scan the port in the range 31000 and 32000. We use nmap as the command to scan the port.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/94224a9c-b602-4149-963c-f3865d0681e6)
After giving the nmap command it displays a list of those ports that are open.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/9f412a91-c7d3-4128-8ac1-0ddfee190c16)
Ports that are open and speak ssl can be identified. From this list, it is clearly given that 31790 port is open and its service is ssl/unknown.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/88a7516c-3956-427a-847d-9553a8d4d417)
On realizing that 31790 port is the right one, I gave the command ''' openssl s_client -connect localhost 31790 ''' to connect to the port and to retrieve further information.

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/b34d3af3-404a-43b2-96b3-76664c84ed2f)
A RSA private key is displayed.
I stored this private key in a directory called band17.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/f058c37f-a9b8-4de6-8369-7d450771f177)

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/4e6da509-df2e-46ca-ad65-e03781d822b2)
  chmod - change file mode bits
 chmod changes the file mode bits of each given file according to mode, which can be either a symbolic representation of changes to make, or an octal  number  representing the bit pattern for the new mode bits. <br>
 nano  is  a  small and friendly editor.  It copies the look and feel of Pico, but is free software, and implements several features that Pico lacks, such as: opening multiple files, scrolling per line, undo/redo, syntax coloring, line numbering, and soft-wrapping overlong lines.

### Level 17 to Level 18

  diff - compare files line by line <br>
  I used the command diff to read the 2 files and it displayed the passwords.  

![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/87d162de-249e-4da3-a6af-a1363261ad04)

### Level 18 to Level 19

After submitting the password from passwords.new file, I was logged in to bandit18.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/6d9e1813-343b-4f27-a3bb-3a08018ccfb8)
I received the text, "Bye-Bye" at the end. <br>
Later, I gave the command, <br>
'''ssh bandit18@bandit.labs.overthewire.org -p 2220 -t/bin/sh ''' and then read the file readme to get the password for level 19.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/a146cc77-a08a-42d8-969a-ad9d7a539204)


### Level 19 to Level 20

setuid() sets the effective user ID of the calling process.
On giving the ls -la command it displayed a list, where ./bandit20-d0 was highlighted. I used the cat command to read the password. 
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/450f298c-b95f-44ff-af39-90b23c921479)

### Level 20 to Level 21
While browsing about the nc command, I understood that netcat command is a simple unix utility that reads and writes data across network connections using TCP, UDP protocol.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/e291e718-19d8-49d7-a9b7-d3ccefc07d0a)
In another terminal, I used the nc -lvp command with a random port number which is 9999, in my case. This port was connected with the ./suconnect file and after submitting the level 20 password, I got the password to the next level.
![image](https://github.com/BuenaPeninnahQuadros/overthewire_bandit_writeup/assets/85785379/b8bde404-599c-429e-ba9d-5f646a0edca0)























