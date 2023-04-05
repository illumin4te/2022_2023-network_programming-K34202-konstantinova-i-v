University: ITMO University Faculty: FICT Course: Network programming Year: 2022/2023 Group: K34202 Author: Konstantinova Iuliia Vyacheslavovna Lab: Lab1 Date of create: 01.02.2023 Date of finished: 

Цель: развернуть виртуальную машину на базе платформы Microsoft Azure с установленной системой контроля конфигураций Ansible и установить CHR в VirtualBox

Ход работы:

В начале работы создана виртуальная машина в Яндекс.Облаке на операционной системе Ubuntu. На ней установлены python3 и Ansible при помощи команд (Рис.1): 

sudo apt install python3-pip

ls -la /usr/bin/python3.6

sudo pip3 install ansible

ansible –version
 
 ![image](https://user-images.githubusercontent.com/90499135/230172200-3b25c9dc-17eb-4fa3-be55-640fe860331c.png)

Рисунок 1 – Установка Ansible

Далее в VirtualBox выполнена установка CHR (RouterOS).
После этого создан Wireguard/OpenVPN/L2TP сервер для организации VPN туннеля между сервером автоматизации, где была установлена система контроля конфигураций Ansible, и локальным CHR. Для этого в VirtualBox устанавлен MikroTik 7 версии (Рис.2). Установлен Wireguard на удалённую машину, в нём прописан в файл условий интерфейса. Создана пара ключей.

 ![image](https://user-images.githubusercontent.com/90499135/230164152-142676b6-a167-4907-8b3d-c8d477e13cd0.png)

Рисунок 2 – MikroTik 

Поскольку в качестве VPN был выбран WireGuard, и установлен MikroTik последней версии, в настройках Wireguard создан новый интерфейс. Заполнены строки: MTU оставлен как указано, ListenPort получен командой вывода файла /etc/wireguard/wg0.conf на сервере, ключи сгененрированы автоматически (Рис.3).
 
 ![image](https://user-images.githubusercontent.com/90499135/230164179-d4b2fe2c-098f-4a52-b7c0-eeda52ed460b.png)

Рисунок 3 – WireGuard 

Затем создан Peer с указанием созданного интерфейса, публичного ключа сервера, публичного IP, порта и сети адресов для подключения. В настройке IP - Addresses указаны выбранная сеть и созданный интерфейс (Рис.4).
 
 ![image](https://user-images.githubusercontent.com/90499135/230164200-a28d4beb-bfba-4773-b495-94a133d58c2b.png)

Рисунок 4 – Указание сети и интерфейса

В настройке IP - Firewall создан NAT Rule masquerade, Masquerade NAT позволяет преобразовывать несколько IP-адресов в другой одиночный IP-адрес. Затем для проверки работоспособности запущен ping к виртуальной машине по заданному IP адресу. Пинг идёт, что показывает, что все настройки выполнены корректно (Рис.5).
 
 ![image](https://user-images.githubusercontent.com/90499135/230164228-588d962b-cc4a-441a-907c-8a2234a1ad40.png)

Рисунок 5 – Проверка работоспособности

В результате выполнения работы создана сеть, соответствующая данной схеме (Рис.6).
 
 ![image](https://user-images.githubusercontent.com/90499135/230164269-31366bea-fdc9-4512-9f5f-e66516d8ef7f.png)

Рисунок 6 – Схема сети

Вывод: в ходе выполнения работы все задачи выполнены, а именно при помощи WireGuard настроен VPN туннель между виртуальной машиной с операционной системой RouterOS и удалённой виртуальной машиной. 
