# Сетевые пакеты. VLAN'ы. LACP

## Задание выполнялось с использованием VirtualBox 6.1.40, использовался vagrant с box-образом generic/debian11

## Задание:
в Office1 в тестовой подсети появляется сервера с доп интерфесами и адресами
в internal сети testLAN

    testClient1 - 10.10.10.254
    testClient2 - 10.10.10.254
    testServer1- 10.10.10.1
    testServer2- 10.10.10.1
    развести вланами
    testClient1 <-> testServer1
    testClient2 <-> testServer2
    между centralRouter и inetRouter
    "пробросить" 2 линка (общая inernal сеть) и объединить их в бонд
    проверить работу c отключением интерфейсов
