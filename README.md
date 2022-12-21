# ДЗ 2

## Theory

[0.4] What are computer ports on a high level? How many ports are there on a typical computer?

- Порты - откртые каналы связи с внешним миром или LAN, которые система слушает с целью получения сетевых пакетов. Стандартно портов 65 535, некоторые из которых условно "забронированы" под TCP/FTP/SSH и т.п. Например, в нашей общаге похоже был whitelist на порты 443/80, из-за чего не работали стим, ssh и прочее. При обращении к любому устройству/серверу после IP-адреса через : всегда указывается порт. 


[0.4] What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.

[0.4] Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.

- IP - уникальный адрес, на который отправляются пакеты в сети. Публичным IP называют уникальный адрес во внешней сети (Интернете), из-за дефицита ipv4 они меняются динамически, т.к. их пул у провайдеров ограничен (+ используются NAP для шера одного IP на многих пользователей). При вводе буков в адресную строку, браузер сначала обращается к DNS-серверу (например, 1.1.1.1), который в свою очередь даёт IP сервера, на котором хостится поисковая строка (+ DNS балансирует нагрузку, равномерно выдавая юзерам IP разных серверов с одинаковым контентом). Далее на этот IP кидаем GET-запрос и получаем ответ, декодируя пакеты в HTML.


[0.4] What is Nginx? How does it work on the high level? List several alternative web servers.

[0.4] What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.
