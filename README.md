Домашнее задание к занятию «Компьютерные сети. Лекция 1»
Цель задания

В результате выполнения задания вы:

    научитесь работать с HTTP-запросами, чтобы увидеть, как клиенты взаимодействуют с серверами по этому протоколу;
    поработаете с сетевыми утилитами, чтобы разобраться, как их можно использовать для отладки сетевых запросов, соединений.

Чеклист готовности к домашнему заданию

    Убедитесь, что у вас установлены необходимые сетевые утилиты — dig, traceroute, mtr, telnet.
    Используйте apt install для установки пакетов.

Инструкция к заданию

    Создайте .md-файл для ответов на вопросы задания в своём репозитории, после выполнения прикрепите ссылку на него в личном кабинете.
    Любые вопросы по выполнению заданий задавайте в чате учебной группы или в разделе «Вопросы по заданию» в личном кабинете.

Дополнительные материалы для выполнения задания

    Полезным дополнением к обозначенным выше утилитам будет пакет net-tools. Установить его можно с помощью команды apt install net-tools.
    RFC протокола HTTP/1.0, в частности страница с кодами ответа.
    Ссылки на другие RFC для HTTP.

Задание

Шаг 1. Работа c HTTP через telnet.

    Подключитесь утилитой telnet к сайту stackoverflow.com:

telnet stackoverflow.com 80

    Отправьте HTTP-запрос:

GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]

В ответе укажите полученный HTTP-код и поясните, что он означает.
```
Ответ от сервера
HTTP/1.1 403 Forbidden
Connection: close
Content-Length: 1920
Server: Varnish
Retry-After: 0
Content-Type: text/html
Accept-Ranges: bytes
Date: Thu, 30 Mar 2023 08:33:03 GMT
Via: 1.1 varnish
X-Served-By: cache-hel1410022-HEL
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1680165183.213728,VS0,VE1
X-DNS-Prefetch-Control: off

код 403 - доступ к запрошенному ресурсу запрещен 
и далее html код страницы в котором описано что ваш ip адресс заблокирован для досупа к данному сервису и обращаться по такому то емейлу.
```

Шаг 2. Повторите задание 1 в браузере, используя консоль разработчика F12:

    откройте вкладку Network;
    отправьте запрос http://stackoverflow.com;
    найдите первый ответ HTTP-сервера, откройте вкладку Headers;
    укажите в ответе полученный HTTP-код;
    
```
HTTP/2 200 OK
cache-control: private
content-type: text/html; charset=utf-8
content-encoding: gzip
strict-transport-security: max-age=15552000
x-frame-options: SAMEORIGIN
set-cookie: OptanonConsent=; expires=Tue, 28 Mar 2023 08:54:28 GMT; domain=.stackoverflow.com; path=/; secure; samesite=none; httponly
set-cookie: OptanonAlertBoxClosed=; expires=Tue, 28 Mar 2023 08:54:28 GMT; domain=.stackoverflow.com; path=/; secure; samesite=none; httponly
set-cookie: prov_tgt=; expires=Tue, 28 Mar 2023 08:54:28 GMT; domain=.stackoverflow.com; path=/; secure; samesite=none; httponly
x-request-guid: 7f050fb5-907b-48c0-990c-fa0d1c411113
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
accept-ranges: bytes
date: Thu, 30 Mar 2023 08:54:28 GMT
via: 1.1 varnish
x-served-by: cache-hel1410024-HEL
x-cache: MISS
x-cache-hits: 0
x-timer: S1680166469.627911,VS0,VE115
vary: Accept-Encoding,Fastly-SSL
x-dns-prefetch-control: off
X-Firefox-Spdy: h2
```


    проверьте время загрузки страницы и определите, какой запрос обрабатывался дольше всего;
 ```
 TLS
 ```
    приложите скриншот консоли браузера в ответ.
![Скрин браузера](https://github.com/yahanext/devops28-net1/blob/main/scr.png)

Шаг 3. Какой IP-адрес у вас в интернете?
```
95.78.186.142
```
Шаг 4. Какому провайдеру принадлежит ваш IP-адрес? Какой автономной системе AS? Воспользуйтесь утилитой whois.
```
Эр Телеком холдинг
origin:         AS41661
```

Шаг 5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой traceroute.
```
yaha@yahawork:~$ traceroute -An 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  10.66.6.1 [*]  0.174 ms  0.137 ms  0.167 ms
 2  * * *
 3  91.144.134.46 [AS41661]  1.037 ms  1.085 ms  1.044 ms
 4  72.14.215.165 [AS15169]  22.665 ms  22.593 ms  22.623 ms
 5  72.14.215.166 [AS15169]  23.532 ms  23.475 ms  23.417 ms
 6  * * *
 7  108.170.227.70 [AS15169]  22.990 ms 172.253.69.166 [AS15169]  22.745 ms 72.14.239.130 [AS15169]  22.931 ms
 8  108.170.250.146 [AS15169]  26.526 ms 108.170.250.99 [AS15169]  27.269 ms  27.214 ms
 9  142.251.238.82 [AS15169]  39.908 ms 142.250.238.214 [AS15169]  39.470 ms 142.251.238.82 [AS15169]  39.797 ms
10  66.249.95.224 [AS15169]  36.144 ms  38.709 ms 72.14.235.69 [AS15169]  37.897 ms
11  216.239.57.5 [AS15169]  36.018 ms 216.239.40.61 [AS15169]  38.769 ms 216.239.62.9 [AS15169]  37.196 ms
12  * * *
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  8.8.8.8 [AS15169/AS263411]  38.454 ms  36.772 ms  36.892 ms
```


Шаг 6. Повторите задание 5 в утилите mtr. На каком участке наибольшая задержка — delay?
```
AS15169 142.250.209.25
```
Шаг 7. Какие DNS-сервера отвечают за доменное имя dns.google? Какие A-записи? Воспользуйтесь утилитой dig.
```
dns.google.		11664	IN	NS	ns4.zdns.google.
dns.google.		11664	IN	NS	ns2.zdns.google.
dns.google.		11664	IN	NS	ns1.zdns.google.
dns.google.		11664	IN	NS	ns3.zdns.google.

;; ADDITIONAL SECTION:
ns3.zdns.google.	42243	IN	A	216.239.36.114

A записи
;dns.google.			IN	A

;; ANSWER SECTION:
dns.google.		55	IN	A	8.8.8.8
dns.google.		55	IN	A	8.8.4.4
```

Шаг 8. Проверьте PTR записи для IP-адресов из задания 7. Какое доменное имя привязано к IP? Воспользуйтесь утилитой dig.
```
;dns.google.			IN	PTR

;; AUTHORITY SECTION:
dns.google.		300	IN	SOA	ns1.zdns.google. cloud-dns-hostmaster.google.com. 1 21600 3600 259200 300
```


В качестве ответов на вопросы приложите лог выполнения команд в консоли или скриншот полученных результатов.
Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.
Критерии оценки

Зачёт:

    выполнены все задания;
    ответы даны в развёрнутой форме;
    приложены соответствующие скриншоты и файлы проекта;
    в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

    задание выполнено частично или не выполнено вообще;
    в логике выполнения заданий есть противоречия и существенные недостатки.
