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
При сканировании через nmap в логах fail2ban ничего не записывалось
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

--------------
fail2ban - активность гидры моментально была обнаружена и ip адрес был отправлен в бан

```
2026-08-28 23:20:46,849 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,850 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,850 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,851 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,851 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,851 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,852 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,852 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,853 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,853 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,853 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,854 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,854 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,855 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,855 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:46,855 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:46
2026-08-28 23:20:47,634 fail2ban.actions        [6638]: NOTICE  [sshd] Ban 10.0.2.15
2026-08-28 23:20:48,379 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:47
2026-08-28 23:20:48,380 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,380 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,679 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,680 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,680 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,680 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,680 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,681 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,681 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,996 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,996 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,996 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,996 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:48,997 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:48
2026-08-28 23:20:49,379 fail2ban.filter         [6638]: INFO    [sshd] Found 10.0.2.15 - 2026-08-28 23:20:49
```

suricata - так же была обнаружена подозрительная активность на 22 порту ssh

```
08/28/2026-23:20:52.551507  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56627 -> 10.0.2.4:22
08/28/2026-23:20:54.572881  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56618 -> 10.0.2.4:22
08/28/2026-23:20:54.736384  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56616 -> 10.0.2.4:22
08/28/2026-23:20:55.663792  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56627 -> 10.0.2.4:22
08/28/2026-23:20:56.714978  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56631 -> 10.0.2.4:22
08/28/2026-23:20:56.916724  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56637 -> 10.0.2.4:22
08/28/2026-23:20:57.734235  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56635 -> 10.0.2.4:22
08/28/2026-23:20:58.488767  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56632 -> 10.0.2.4:22
08/28/2026-23:20:59.335922  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56639 -> 10.0.2.4:22
08/28/2026-23:21:02.601910  [**] [1:2003068:7] ET SCAN Potential SSH Scan OUTBOUND [**] [Classification: Attempted Information Leak] [Priority: 2] {TCP} 10.0.2.15:56634 -> 10.0.2.4:22
```