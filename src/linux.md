## Part 1. Инструмент ipcalc

### 1.1. Сети и маски

#### Определить и записать в отчёт:

##### 1) Адрес сети 192.167.38.54/13
- 192.160.0.0/13


##### 2) Перевод маски 255.255.255.0 в префиксную и двоичную запись, /15 в обычную и двоичную, 11111111.11111111.11111111.11110000 в обычную и префиксную
##### маска 255.255.255.0
- префиксная - /24;
- двоичная - 11111111.11111111.11111111.00000000;

##### маска /15
- обычная 255.254.0.0;
- двоичная - 11111111.11111110.00000000.00000000;

##### маска 11111111.11111111.11111111.11110000;
- обычная 255.255.255.240;
- префиксная /28

##### 3) Минимальный и максимальный хост в сети 12.167.38.4 при масках: /8, 11111111.11111111.00000000.00000000, 255.255.254.0 и /4
- Максимальный IP 12.167.38.254; Минимальный IP	12.167.38.1 (/8);
- Максимальный IP 12.167.255.254; Минимальный IP 12.167.0.1 (11111111.11111111.00000000.00000000)(/16);
- Максимальный IP 12.167.39.254; Минимальный IP	12.167.38.1 (255.255.254.0)(/23);
- Максимальный IP 15.255.255.254; Минимальный IP 0.0.0.1 (/4);


### 1.2. localhost

#### Определить и записать в отчёт, можно ли обратиться к приложению, работающему на localhost, со следующими IP: 194.34.23.100, 127.0.0.2, 127.1.0.1, 128.0.0.1

- По адресам 194.34.23.100/16 и 128.0.0.1/8 обратиться к приложению не получится, потому что у них нет петли.
- У 127.0.0.2/24 и 127.1.0.1/8 есть loopback, так что к ним обратиться можно.


### 1.3. Диапазоны и сегменты сетей

#### Определить и записать в отчёт:

##### 1) какие из перечисленных IP можно использовать в качестве публичного, а какие только в качестве частных: 10.0.0.45, 134.43.0.2, 192.168.4.2, 172.20.250.4, 172.0.2.1, 192.172.0.1, 172.68.0.2, 172.16.255.255, 10.10.10.10, 192.169.168.1

##### - В качестве частных: 
- 10.0.0.45 
- 192.168.4.2
- 172.20.250.4
- 172.16.255.255
- 10.10.10.10


##### 2) какие из перечисленных IP адресов шлюза возможны у сети 10.10.0.0/18: 10.0.0.1, 10.10.0.2, 10.10.10.10, 10.10.100.1, 10.10.1.255
- 10.10.0.2
- 10.10.10.10
- 10.10.1.255

## Part 2. Статическая маршрутизация между двумя машинами

#### Поднять две виртуальные машины (далее -- ws1 и ws2)

#### С помощью команды ip a посмотреть существующие сетевые интерфейсы

![linux](images/ip_a.png "Сетевой Интерфейс")


#### Описать сетевой интерфейс, соответствующий внутренней сети, на обеих машинах и задать следующие адреса и маски: ws1 - 192.168.100.10, маска /16, ws2 - 172.24.116.8, маска /12

- В отчёт поместить скрины с содержанием изменённого файла etc/netplan/00-installer-config.yaml для каждой машины.

- ws1:
![linux](images/interface1.png "Интерфейс1")

- ws2:
![linux](images/interface2.png "Интерфейс2")

#### Выполнить команду netplan apply для перезапуска сервиса сети

- В отчёт поместить скрин с вызовом и выводом использованной команды.

- ws1:
![linux](images/commands1.png "Команды1")

- ws2:
![linux](images/commands2.png "Команды2")

### 2.1. Добавление статического маршрута вручную

#### Добавить статический маршрут от одной машины до другой и обратно при помощи команды вида ip r add

#### Пропинговать соединение между машинами

- ws1:
![linux](images/ping1.png "Ping_connection_commands1")

- ws2:
![linux](images/ping2.png "Ping_connection_commands2")

### 2.2. Добавление статического маршрута с сохранением

#### Перезапустить машины

#### Добавить статический маршрут от одной машины до другой с помощью файла etc/netplan/00-installer-config.yaml

- ws1:
![linux](images/interface11.png "interface11")

- ws2:
![linux](images/interface22.png "interface22")

#### Пропинговать соединение между машинами
- ws1:
![linux](images/ping11.png "ping11")

- ws2:
![linux](images/ping22.png "ping22")


## Part 3. Утилита iperf3

### 3.1. Скорость соединения

#### Перевести и записать в отчёт: 8 Mbps в MB/s, 100 MB/s в Kbps, 1 Gbps в Mbps
- 8 Mbps = 1 MB/s
- 100 MB/s = 800000 Kbps
- 1 Gbps = 1000 Mbps

### 3.2. Утилита iperf3

#### Измерить скорость соединения между ws1 и ws2
- В отчёт поместить скрины с вызовом и выводом использованных команд.Part 3. Утилита iperf3
- ws1:
![linux](images/iperf31.png "iperf3")

-ws2:
![linux](images/iperf32.png "iperf22")


## Part 4. Сетевой экран

### 4.1. Утилита iptables


#### Создать файл /etc/firewall.sh, имитирующий фаерволл, на ws1 и ws2:
- #!/bin/sh

- iptables –F
- iptables -X

#### Нужно добавить в файл подряд следующие правила:

#### 1) на ws1 применить стратегию когда в начале пишется запрещающее правило, а в конце пишется разрешающее правило (это касается пунктов 4 и 5)

#### 2) на ws2 применить стратегию когда в начале пишется разрешающее правило, а в конце пишется запрещающее правило (это касается пунктов 4 и 5)

#### 3) открыть на машинах доступ для порта 22 (ssh) и порта 80 (http)

#### 4) запретить echo reply (машина не должна "пинговаться”, т.е. должна быть блокировка на OUTPUT)

#### 5) разрешить echo reply (машина должна "пинговаться")

- ##### ws1:
![linux](images/iptables1.png "iptables1")

- ##### ws2:
![linux](images/iptables2.png "iptables2")


#### Запустить файлы на обеих машинах командами chmod +x /etc/firewall.sh и /etc/firewall.sh

- ##### ws1:
![linux](images/firewallsh1.png "Запуск скрипта firewall1")

- ##### ws2:
![linux](images/firewallsh2.png "Запуск скрипта firewall2")

- Разница в стратегиях заключается в том, что изначально в машине ws-1 мы сначала разрешаем, а после запрещаем вывод ping'a. В машине ws2 всё ровным счетом наоборот.

#### 4.2. Утилита nmap


##### Командой ping найти машину, которая не "пингуется", после чего утилитой nmap показать, что хост машины запущен
- Проверка: в выводе nmap должно быть сказано: Host is up

![linux](images/nmap.png "nmap хост запущен")

## Part 5. Статическая маршрутизация сети

### 5.1. Настройка адресов машин

- r1
![linux](images/r1.png "r1")

- r2
![linux](images/r2.png "r2")

- ws11
![linux](images/ws11.png "ws11")

- ws21
![linux](images/ws21.png "ws21")

- ws22
![linux](images/ws22.png "ws22")


#### Перезапустить сервис сети. Если ошибок нет, то командой ip -4 a проверить, что адрес машины задан верно. Также пропинговать ws22 с ws21. Аналогично пропинговать r1 с ws11.

![linux](images/ws11ping.png "ws11ping")
![linux](images/ws22ping.png "ws22ping")

### 5.2. Включение переадресации IP-адресов.

#### Для включения переадресации IP, выполните команду на роутерах: sysctl -w net.ipv4.ip_forward=1.При таком подходе переадресация не будет работать после перезагрузки системы.

- r1
![linux](images/sysctl1.png "sysctl1(Переадресация не работает после перезагрузк)")

- r2
![linux](images/sysctl2.png "sysctl2(Переадресация не работает после перезагрузк)")


#### Откройте файл /etc/sysctl.conf и добавьте в него следующую строку: net.ipv4.ip_forward = 1. При использовании этого подхода, IP-переадресация включена на постоянной основе.

- r1
![linux](images/forward1.png "Переадресация включена на постоянке r1")

- r2
![linux](images/forward2.png "Переадресация включена на постоянке r2")


### 5.3. Установка маршрута по-умолчанию
Пример вывода команды ip r после добавления шлюза:
default via 10.10.0.1 dev eth0
10.10.0.0/18 dev eth0 proto kernel scope link src 10.10.0.2

#### Настроить маршрут по-умолчанию (шлюз) для рабочих станций. Для этого добавить default перед IP роутера в файле конфигураций

- r1
![linux](images/r1_default.png "Задается default шлюз r1")
- r2
![linux](images/r2_default.png "Задается default шлюз r2")
- ws11
![linux](images/ws11_default.png "Задается default шлюз ws11")
- ws21
![linux](images/ws21_default.png "Задается default шлюз ws21")
- ws22
![linux](images/ws22_default.png "Задается default шлюз ws22")


#### Вызвать ip r и показать, что добавился маршрут в таблицу маршрутизации

- r1
![linux](images/r1_ip_r.png "ip r (r1)")
- r2
![linux](images/r2_ip_r.png "ip r r2")
- ws11
![linux](images/ws11_ip_r.png "ip r ws11")
- ws21
![linux](images/ws21_ip_r.png "ip r ws21")
- ws22
![linux](images/ws22_ip_r.png "ip r ws22")

#### Пропинговать с ws11 роутер r2 и показать на r2, что пинг доходит. Для этого использовать команду: tcpdump -tn -i eth1

- ws11
![linux](images/ping_ws1_to_r2.png "ping ws1 to r2")
- r2
![linux](images/r2_tcdump.png "tcdump r2")
### 5.4. Добавление статических маршрутов

#### Добавить в роутеры r1 и r2 статические маршруты в файле конфигураций. Пример для r1 маршрута в сетку 10.20.0.0/26:
#### Добавить в конец описания сетевого интерфейса eth1:
- to: 10.20.0.0
  via: 10.100.0.12

- r1
![linux](images/r1_routes.png "r1_routes")
- r2
![linux](images/r2_routes.png "r2_routes")


#### Вызвать ip r и показать таблицы с маршрутами на обоих роутерах. Пример таблицы на r1:
#### 10.100.0.0/16 dev eth1 proto kernel scope link src 10.100.0.11
#### 10.20.0.0/26 via 10.100.0.12 dev eth1
#### 10.10.0.0/18 dev eth0 proto kernel scope link src 10.10.0.1

- r1
![linux](images/ip_r_r1.png "ip_r_r1")
- r2
![linux](images/ip_r_r2.png "ip_r_r2")


#### Запустить команды на ws11:
#### ip r list 10.10.0.0/[маска сети] и ip r list 0.0.0.0/0

- ws11
![linux](images/ws11_ip_r_list.png "ws11_ip_r_list")
- Выбран путь отличный от 10.10.0.0 потому что этот адрес указывает на все адреса.

### 5.5. Построение списка маршрутизаторов
#### Пример вывода утилиты traceroute после добавления шлюза:
#### 1 10.10.0.1 0 ms 1 ms 0 ms
#### 2 10.100.0.12 1 ms 0 ms 1 ms
#### 3 10.20.0.10 12 ms 1 ms 3 ms

#### Запустить на r1 команду дампа:
#### tcpdump -tnv -i eth0

#### При помощи утилиты traceroute построить список маршрутизаторов на пути от ws11 до ws21

- r1
![linux](images/r1_tcpdump.png "tcpdump_r1")
- ws11
![linux](images/traceroute_ws11_ws21.png "traceroute ws11 to ws21")
- Путь строиться от узла к узлу до того момента, покаа не будет достигнута конечная точка. Каждый пакет проходит на своем пути определенное количество узлов, пока достигнет своей цели. На каждом узле добавляется счетчик, который отслеживает количество пройденых узлов.

### 5.6. Использование протокола ICMP при маршрутизации

#### Запустить на r1 перехват сетевого трафика, проходящего через eth0 с помощью команды:
#### tcpdump -n -i eth0 icmp

#### Пропинговать с ws11 несуществующий IP (например, 10.30.0.111) с помощью команды:
#### ping -c 1 10.30.0.111

- r1:
![linux](images/r1_tcpdump_icmp.png "r1_tcpdump")
- ws11:
![linux](images/ping_nothing.png "ping 10.30.0.111")


## Part 6. Динамическая настройка IP с помощью DHCP

#### Для r2 настроить в файле /etc/dhcp/dhcpd.conf конфигурацию службы DHCP:

#### 1) указать адрес маршрутизатора по-умолчанию, DNS-сервер и адрес внутренней сети. Пример файла для r2:
subnet 10.100.0.0 netmask 255.255.0.0 {}

subnet 10.20.0.0 netmask 255.255.255.192
{
    range 10.20.0.2 10.20.0.50;
    option routers 10.20.0.1;
    option domain-name-servers 10.20.0.1;
}

#### 2) в файле resolv.conf прописать nameserver 8.8.8.8.
- 1)
![linux](images/r2_dhcpd.conf.png "dhcpd.conf")
- 2)
![linux](images/r2_resolv.conf.png "resolv.conf")


#### Перезагрузить службу DHCP командой systemctl restart isc-dhcp-server. Машину ws21 перезагрузить при помощи reboot и через ip a показать, что она получила адрес. Также пропинговать ws22 с ws21.

![linux](images/restart_DHCP.png "restart_DHCP")
![linux](images/ws21_ip_a.png "ws21_ip_a")
![linux](images/ping_ws21_to_ws22.png "ping_ws21_to_ws22")

#### Указать MAC адрес у ws11, для этого в etc/netplan/00-installer-config.yaml надо добавить строки: macaddress: 10:10:10:10:10:BA, dhcp4: true

![linux](images/macaddress_ws11.png "macaddress_ws11")

#### Для r1 настроить аналогично r2, но сделать выдачу адресов с жесткой привязкой к MAC-адресу (ws11). Провести аналогичные тесты

![linux](images/r1_dhcpd.conf.png "dhcpd.conf")

![linux](images/r1_resolv.conf.png "resolv.conf")

![linux](images/macaddress_ws11.png "macaddress_ws11")


#### Запросить с ws21 обновление ip адреса

![linux](images/r1_ws21_ip_a_old.png "old ip")

![linux](images/r1_ws21_ip_a_new.png "new ip")

- Использовал:
- sudo dhclient -v
- sudp dhclietn -r
- sudo dhclient -v

## Part 7. NAT

- Ну и, наконец, в качестве вишенки на торте, я расскажу тебе про механизм преобразования адресов.
== Задание ==
В данном задании используются виртуальные машины из Части 5

#### В файле /etc/apache2/ports.conf на ws22 и r1 изменить строку Listen 80 на Listen 0.0.0.0:80, то есть сделать сервер Apache2 общедоступным

![linux](images/ws22_apache2.png "ws22_apache2")


#### Запустить веб-сервер Apache командой service apache2 start на ws22 и r1
- ws22
![linux](images/ws22_start_apache2.png "ws22_start_apache2")
- r1
![linux](images/r1_start_apache2.png "r1_start_apache2")

#### Добавить в фаервол, созданный по аналогии с фаерволом из Части 4, на r2 следующие правила:

#### 1) Удаление правил в таблице filter - iptables -F


#### 2) Удаление правил в таблице "NAT" - iptables -F -t nat


#### 3) Отбрасывать все маршрутизируемые пакеты - iptables --policy FORWARD DROP


#### Запускать файл также, как в Части 4

#### Проверить соединение между ws22 и r1 командой ping

#### При запуске файла с этими правилами, ws22 не должна "пинговаться" с r1

![linux](images/ping_ws22_to_r1.png "ping_ws22_to_r1")

#### Добавить в файл ещё одно правило:

#### 4) Разрешить маршрутизацию всех пакетов протокола ICMP

#### Запускать файл также, как в Части 4

#### Проверить соединение между ws22 и r1 командой ping

#### При запуске файла с этими правилами, ws22 должна "пинговаться" с r1

![linux](images/ping_ws22_to_r1_2.png "ping_ws22_to_r1_2")


#### Добавить в файл ещё два правила:

#### 5) Включить SNAT, а именно маскирование всех локальных ip из локальной сети, находящейся за r2 (по обозначениям из Части 5 - сеть 10.20.0.0)
#### Совет: стоит подумать о маршрутизации внутренних пакетов, а также внешних пакетов с установленным соединением

#### 6) Включить DNAT на 8080 порт машины r2 и добавить к веб-серверу Apache, запущенному на ws22, доступ извне сети
#### Совет: стоит учесть, что при попытке подключения возникнет новое tcp-соединение, предназначенное ws22 и 80 порту

![linux](images/config.sh_r2.png "config.sh_r2")

#### Запускать файл также, как в Части 4
#### Перед тестированием рекомендуется отключить сетевой интерфейс NAT (его наличие можно проверить командой ip a) в VirtualBox, если он включен

#### Проверить соединение по TCP для SNAT, для этого с ws22 подключиться к серверу Apache на r1 командой:
#### telnet [адрес] [порт]

#### Проверить соединение по TCP для DNAT, для этого с r1 подключиться к серверу Apache на ws22 командой telnet (обращаться по адресу r2 и порту 8080)

![linux](images/telnet_1.png "telnet_1")
![linux](images/telnet_2.png "telnet_2")

Сохранить дампы образов виртуальных машин
p.s. Ни в коем случае не сохранять дампы в гит!

## Part 8. Дополнительно. Знакомство с SSH Tunnels


#### Запустить на r2 фаервол с правилами из Части 7

#### Запустить веб-сервер Apache на ws22 только на localhost (то есть в файле /etc/apache2/ports.conf изменить строку Listen 80 на Listen localhost:80)

#### Воспользоваться Local TCP forwarding с ws21 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws21

#### Воспользоваться Remote TCP forwarding c ws11 до ws22, чтобы получить доступ к веб-серверу на ws22 с ws11

#### Для проверки, сработало ли подключение в обоих предыдущих пунктах, перейдите во второй терминал (например, клавишами Alt + F2) и выполните команду:
#### telnet 127.0.0.1 [локальный порт]

- ssh -L
- ssh -R
![linux](images/telnet_3.png "telnet_3")
![linux](images/telnet_4.png "telnet_4")

Сохранить дампы образов виртуальных машин
p.s. Ни в коем случае не сохранять дампы в гит!
