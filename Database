•	Instalasi paket paket dari yang pertama install apache, php, dan mariadb.
root@debian:~# apt install -y apache2 apache2-utils

root@debian:~# apt install -y php php-mysql php-mbstring

root@debian:~# apt install -y mariadb-server mariadb-client

•	Setelah itu lakukan mysq secure instalation
root@debian:~# mysql_secure_installation
untuk bagian pertama saat disuruh sistem mmemasukan password di enter saja
New password: tekaje
Re-enter new password: tekaje
Password updated successfully!
Reloading privilege tables..
Untuk selanjutnya pilih Y (yes) saja 

•	Setelah lakukan instalasi pada PHPMYADMIN nya.
root@debian:~# mkdir download
root@debian:~# cd download/
root@debian:~/download# wget https://files.phpmyadmin.net/phpMyAdmin/4.9.0.1/phpMyAdmin-4.9.0.1-all-languages.tar.gz

•	Ekstrak file phpmyadmin yang telah di download
root@debian:~/download# tar -zxvf phpMyAdmin-4.9.0.1-all-languages.tar.gz

•	Jika sudah maka selanjutnya adalah memindahkan file phpmyadnim yang telah diekstrak ke dalam folder /usr/share/phpMyAdmin
root@debian:~/download# mv phpMyAdmin-4.9.0.1-all-languages /usr/share/phpMyAdmin

•	Langkah berikutnya adalah melakukan copy file config.sample.inc.php menjadi file config.inc.php
root@debian:~/download# cp -pr /usr/share/phpMyAdmin/config.sample.inc.php /usr/share/phpMyAdmin/config.inc.php
•	Jika sudah di copy maka kita akan konfigurasi file tersebut.
root@debian:~/download# nano /usr/share/phpMyAdmin/config.inc.php

$cfg['blowfish_secret'] = 'STRINGOFTHIRTYTWORANDOMCHARACTERS'; /* YOU MUST FILL IN THIS FOR COOKIE AUTH!$

/* User used to manipulate with storage */
 $cfg['Servers'][$i]['controlhost'] = 'localhost';
// $cfg['Servers'][$i]['controlport'] = '';
 $cfg['Servers'][$i]['controluser'] = 'pma';
 $cfg['Servers'][$i]['controlpass'] = 'pmapass';

/* Storage database and tables */
 $cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';
 $cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';
 $cfg['Servers'][$i]['relation'] = 'pma__relation';
 $cfg['Servers'][$i]['table_info'] = 'pma__table_info';
 $cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';
 $cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';
 $cfg['Servers'][$i]['column_info'] = 'pma__column_info';
 $cfg['Servers'][$i]['history'] = 'pma__history';
 $cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';
 $cfg['Servers'][$i]['tracking'] = 'pma__tracking';
 $cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';
 $cfg['Servers'][$i]['recent'] = 'pma__recent';
 $cfg['Servers'][$i]['favorite'] = 'pma__favorite';
 $cfg['Servers'][$i]['users'] = 'pma__users';
 $cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';
 $cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';
$cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';
 $cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';
 $cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';
 $cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';

Kalau sudah jangan lupa di save ctrl+x -> y
•	Jika sudah kita akan membuat table untuk phpMyAdmin berikut tahapannya
root@debian:~/download# mysql < /usr/share/phpMyAdmin/sql/create_tables.sql -u root -p

•	Setelah itu kita akan memberikan akses control agar bisa menggunakan phpMyAdmin nya.
root@debian:~/download# mysql -u root –p
Enter password: tekaje22 (password yang tadi kalian buat)
MariaDB [(none)]> GRANT ALL PRIVILEGES ON phpmyadmin.* TO 'pma'@'localhost' IDENTIFIED BY 'pmapass';
MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> quit

•	Setelah itu kita akan mempublish phpMyAdmin nya agar bisa dibuka di web server kita
root@debian:~# cd /etc/apache2/sites-available/
root@debian:/etc/apache2/sites-available# nano 000-default.conf

Alias /phpmyadmin /usr/share/phpMyAdmin
        
Lalu di save ctrl+x -> y

•	Tahap berikutnya adalah publikasi ke web server file phpmyadmin nya berikut caranya
root@debian:/ # a2ensite 000-default.conf
root@debian:/# mkdir /usr/share/phpMyAdmin/temp
root@debian:/# chmod 777 /usr/share/phpMyAdmin/temp
root@debian:/# chown -R www-data:www-data /usr/share/phpMyAdmin
root@debian:/# systemctl restart apache2

•	Selanjutnya kita akan membuat akses login ke phpmyadmin.
root@debian:/# mysql -p -u root
MariaDB [(none)]> CREATE USER 'tekaje22'@'%' IDENTIFIED BY 'tekaje22';
MariaDB [(none)]> GRANT ALL PRIVILEGES ON *.* TO 'tekaje22'@'%' WITH GRANT OPTION;
MariaDB [(none)]> quit
