# Домашнее задание к занятию «Защита сети» Чепелев Павел

### Задание 1

Проведите разведку системы и определите, какие сетевые службы запущены на защищаемой системе:

**sudo nmap -sA < ip-адрес >**

**sudo nmap -sT < ip-адрес >**

**sudo nmap -sS < ip-адрес >**

**sudo nmap -sV < ip-адрес >**

По желанию можете поэкспериментировать с опциями: https://nmap.org/man/ru/man-briefoptions.html.


*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*
------------
SURICATA

**sudo nmap -sA < ip-адрес >** - ничего не выдает, возможно я как то не правильно настроил

**sudo nmap -sT < ip-адрес >** - видно что суриката обнаружила подозрительный трафик на портах СУБД и сканирование VNC портов

```bash
08/27/2026-23:29:15.299259  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:37292 -> 10.0.2.4:3306
08/27/2026-23:29:15.312218  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:36058 -> 10.0.2.4:1521
08/27/2026-23:29:15.313074  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:47738 -> 10.0.2.4:1433
08/27/2026-23:29:15.326932  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:51414 -> 10.0.2.4:5815
08/27/2026-23:29:15.338045  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:40870 -> 10.0.2.4:5432
```

**sudo nmap -sS < ip-адрес >** - то же самое что и при сканировании -sT

```bash suricata
08/27/2026-23:15:32.376258  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:57483 -> 10.0.2.4:3306
08/27/2026-23:15:34.146360  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:57483 -> 10.0.2.4:1433
08/27/2026-23:15:34.245750  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:57484 -> 10.0.2.4:1433
08/27/2026-23:15:37.028896  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:57483 -> 10.0.2.4:1521
08/27/2026-23:15:50.642466  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:57483 -> 10.0.2.4:5432
08/27/2026-23:15:50.675713  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:57483 -> 10.0.2.4:5810
```

**sudo nmap -sV < ip-адрес >** - то же самое что и при сканировании -sT

```bash
08/27/2026-23:31:08.163507  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP}10.0.2.15:34178 -> 10.0.2.4:3306
08/27/2026-23:31:10.605693  [**] [1:2010939:3] ET SCAN Suspicious inbound to PostgreSQL port 5432 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:34178 -> 10.0.2.4:5432
08/27/2026-23:31:10.616660  [**] [1:2002910:6] ET SCAN Potential VNC Scan 5800-5820 [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:34178 -> 10.0.2.4:5810
08/27/2026-23:31:10.623345  [**] [1:2010935:3] ET SCAN Suspicious inbound to MSSQL port 1433 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:34178 -> 10.0.2.4:1433
08/27/2026-23:31:10.630811  [**] [1:2010936:3] ET SCAN Suspicious inbound to Oracle SQL port 1521 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:34178 -> 10.0.2.4:1521
08/27/2026-23:31:10.830292  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP} 10.0.2.15:38273 -> 10.0.2.4:3306
08/27/2026-23:31:14.148192  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP}10.0.2.15:38274 -> 10.0.2.4:3306
08/27/2026-23:31:14.167887  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP}10.0.2.15:38275 -> 10.0.2.4:3306
08/27/2026-23:31:14.196492  [**] [1:2010937:3] ET SCAN Suspicious inbound to mySQL port 3306 [**] [Classification: Potentially Bad Traffic] [Priority: 2] {TCP}10.0.2.15:38276 -> 10.0.2.4:3306
```
------

### Задание 2

Проведите атаку на подбор пароля для службы SSH:

**hydra -L users.txt -P pass.txt < ip-адрес > ssh**

1. Настройка **hydra**: 
 
 - создайте два файла: **users.txt** и **pass.txt**;
 - в каждой строчке первого файла должны быть имена пользователей, второго — пароли. В нашем случае это могут быть случайные строки, но ради эксперимента можете добавить имя и пароль существующего пользователя.

Дополнительная информация по **hydra**: https://kali.tools/?p=1847.

2. Включение защиты SSH для Fail2Ban:

-  открыть файл /etc/fail2ban/jail.conf,
-  найти секцию **ssh**,
-  установить **enabled**  в **true**.

Дополнительная информация по **Fail2Ban**:https://putty.org.ru/articles/fail2ban-ssh.html.



*В качестве ответа пришлите события, которые попали в логи Suricata и Fail2Ban, прокомментируйте результат.*