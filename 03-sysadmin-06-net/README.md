# Домашнее задание к занятию "3.6. Компьютерные сети, лекция 1"

1. Работа c HTTP через телнет.
- Подключитесь утилитой телнет к сайту stackoverflow.com
`telnet stackoverflow.com 80`
- отправьте HTTP запрос
```bash
GET /questions HTTP/1.0
HOST: stackoverflow.com
[press enter]
[press enter]
```
- В ответе укажите полученный HTTP код, что он означает?

**Ответ на Задание 1**
```bash
➜  ~ telnet stackoverflow.com 80
Trying 151.101.65.69...
Connected to stackoverflow.com.
Escape character is '^]'.
GET /questions HTTP/1.0
HOST: stackoverflow.com

HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
x-request-guid: 0aefa045-d1dc-47a7-b628-ca15eed4b494
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Date: Fri, 18 Feb 2022 20:21:36 GMT
Via: 1.1 varnish
Connection: close
X-Served-By: cache-ams21021-AMS
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1645215697.535541,VS0,VE75
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=7534f433-c38e-df52-277a-de37871a5b71; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```
Полученный код означает:
- 301 Moved Permanently - страница перемещена
- location: https://stackoverflow.com/questions - локация уже по https, по Telnet не зайти
- Connection: close - соединение закрыто

2. Повторите задание 1 в браузере, используя консоль разработчика F12.
- откройте вкладку `Network`
- отправьте запрос http://stackoverflow.com
- найдите первый ответ HTTP сервера, откройте вкладку `Headers`
- укажите в ответе полученный HTTP код. - **301**
- проверьте время загрузки страницы - **Load: 1.17 s**, какой запрос обрабатывался дольше всего? - **420 ms загрузка 54.3kB документа _stackoverflow.com/_**
- приложите скриншот консоли браузера в ответ.

```bash
Request URL: http://stackoverflow.com/
Request Method: GET
Status Code: 301 Moved Permanently
Remote Address: 151.101.65.69:80
Referrer Policy: strict-origin-when-cross-origin
```

![Image alt](https://github.com/alexeyandm/my_sysadm-homeworks/raw/devsys10/03-sysadmin-06-net/https_req1.png)

3. Какой IP адрес у вас в интернете? - **176.123.219.239**

4. Какому провайдеру принадлежит ваш IP адрес? Какой автономной системе AS? Воспользуйтесь утилитой `whois`
**netname: INDIKOM-NET**
**origin: AS59584**

5. Через какие сети проходит пакет, отправленный с вашего компьютера на адрес 8.8.8.8? Через какие AS? Воспользуйтесь утилитой `traceroute`

**Сети указаны ниже, но определение  AS - не поддерживается**
```bash
~ traceroute -An 8.8.8.8 
traceroute: n: Unknown host
traceroute: as_setup failed, AS# lookups disabled
traceroute to 8.8.8.8 (8.8.8.8), 64 hops max, 52 byte packets
 1  192.168.1.1 (192.168.1.1)  2.301 ms  2.446 ms  1.234 ms
 2  sco1.br1.myth1.ip.indikom.ru (176.123.216.135)  5.080 ms  2.421 ms  6.129 ms
 3  te1-1.br1.myth1.ip.indikom.ru (176.123.216.133)  1.732 ms  5.833 ms  2.993 ms
 4  176.123.216.72 (176.123.216.72)  1.636 ms  1.800 ms  1.607 ms
 5  gw6.indikom.mtw.ru (185.148.36.17)  2.196 ms  4.123 ms  1.936 ms
 6  72.14.202.188 (72.14.202.188)  3.571 ms  5.128 ms  3.619 ms
 7  * * *
 8  72.14.233.90 (72.14.233.90)  9.275 ms
    108.170.250.129 (108.170.250.129)  4.535 ms
    108.170.225.36 (108.170.225.36)  3.956 ms
 9  108.170.250.146 (108.170.250.146)  6.847 ms *
    108.170.250.66 (108.170.250.66)  4.391 ms
10  * 209.85.255.136 (209.85.255.136)  23.435 ms
    142.251.49.24 (142.251.49.24)  17.044 ms
11  172.253.65.82 (172.253.65.82)  17.364 ms
    172.253.66.110 (172.253.66.110)  19.472 ms
    216.239.43.20 (216.239.43.20)  20.310 ms
12  172.253.51.241 (172.253.51.241)  18.484 ms
    216.239.57.5 (216.239.57.5)  21.362 ms
    216.239.56.101 (216.239.56.101)  25.158 ms
13  * * *
14  * * *
15  * * *
16  * * *
17  * * *
18  * * *
19  dns.google (8.8.8.8)  21.537 ms * *
```

6. Повторите задание 5 в утилите `mtr`. На каком участке наибольшая задержка - delay?

**По параметру 'Avg — среднее время задержки' - худшее время у последнего 21-го хопа на AS15169**

![Image alt](https://github.com/alexeyandm/my_sysadm-homeworks/raw/devsys10/03-sysadmin-06-net/mtr.png)


7. Какие DNS сервера отвечают за доменное имя dns.google? Какие A записи? воспользуйтесь утилитой `dig`
```bash
 ~ dig google.com ANY
...
;; ANSWER SECTION:
google.com.		226	IN	A	64.233.164.100
google.com.		226	IN	A	64.233.164.101
google.com.		226	IN	A	64.233.164.113
google.com.		226	IN	A	64.233.164.102
google.com.		226	IN	A	64.233.164.139
google.com.		226	IN	A	64.233.164.138
google.com.		45	IN	AAAA	2a00:1450:4010:c07::8b
google.com.		45	IN	AAAA	2a00:1450:4010:c07::64
google.com.		45	IN	AAAA	2a00:1450:4010:c07::65
google.com.		45	IN	AAAA	2a00:1450:4010:c07::71


➜  ~ dig dns.google    
...
;; ANSWER SECTION:
dns.google.		623	IN	A	8.8.4.4
dns.google.		623	IN	A	8.8.8.8
```

8. Проверьте PTR записи для IP адресов из задания 7. Какое доменное имя привязано к IP? воспользуйтесь утилитой `dig`
```bash
~ dig -x 8.8.4.4    
...
;; ANSWER SECTION:
4.4.8.8.in-addr.arpa.	41039	IN	PTR	dns.google.

~ dig -x 8.8.8.8
...
;; ANSWER SECTION:
8.8.8.8.in-addr.arpa.	57825	IN	PTR	dns.google.
```
В качестве ответов на вопросы можно приложите лог выполнения команд в консоли или скриншот полученных результатов.

