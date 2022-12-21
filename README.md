# ДЗ 2

## Theory

[0.4] What are computer ports on a high level? How many ports are there on a typical computer?

- Порты - откртые каналы связи с внешним миром или LAN, которые система слушает с целью получения сетевых пакетов. Стандартно портов 65 535, некоторые из которых условно "забронированы" под TCP/FTP/SSH и т.п. Например, в нашей общаге похоже был whitelist на порты 443/80, из-за чего не работали стим, ssh и прочее. При обращении к любому устройству/серверу после IP-адреса через : всегда указывается порт. 


[0.4] What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.

[0.4] Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.

- IP - уникальный адрес, на который отправляются пакеты в сети. Публичным IP называют уникальный адрес во внешней сети (Интернете), из-за дефицита ipv4 они меняются динамически, т.к. их пул у провайдеров ограничен (+ используются NAP для шера одного IP на многих пользователей). При вводе буков в адресную строку, браузер сначала обращается к DNS-серверу (например, 1.1.1.1), который в свою очередь даёт IP сервера, на котором хостится поисковая строка (+ DNS балансирует нагрузку, равномерно выдавая юзерам IP разных серверов с одинаковым контентом). Далее на этот IP кидаем GET-запрос и получаем ответ, декодируя пакеты в HTML.


[0.4] What is Nginx? How does it work on the high level? List several alternative web servers.

[0.4] What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.


## Remote Server:


[2] Create a new virtual machine in the Yandex/Mail/etc cloud (order at least 10GB of free disk space). Generate SSH key pair and use it to connect to your server.

[1] Download the latest human genome assembly (GRCh38) from the Ensemble FTP server (fasta, GFF3). Index the fasta using samtools (samtools faidx) and GFF3 using tabix.

[1] Select and download BED files for three ChIP-seq and one ATAC-seq experiment from the ENCODE (use one tissue/cell line). Sort, bgzip, and index them using tabix.



## JBrowse 2


[1] Download and install JBrowse 2. Create a new jbrowse repository in /mnt/JBrowse/ (or some other folder).

[0.25] Install nginx and amend its config(/etc/nginx/nginx.conf) to contain the following section:


'''
http {
# Don't touch other options!
# ........
# ........

# Add this:
server {
      listen 80;
      index index.html;

      location /jbrowse/ {
          alias /mnt/JBrowse/;    
      }
  }

# ........
}

'''


[0.25] Restart the nginx (reload its config) and make sure that you can access the browser using a link like this: http://64.129.58.13/jbrowse/. Here 64.129.58.13 is your public IP address.

[1] Add your files (BED & FASTA & GFF3) to the genome browser and verify that everything works as intended. Don't forget to index the genome annotation, so you could later search by gene names.
