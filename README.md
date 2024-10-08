# практика


Подготовка

   Для проведения тестов подготовим виртуальную машину VirtualBox на Windows 10 [Version 10.0.19045.4291]
   
   ![image](https://github.com/user-attachments/assets/32a5fd1d-b769-4284-8b78-272c2e5625e9)
   
   ![image](https://github.com/user-attachments/assets/5096d945-8df8-4b43-8864-996ee3b8e23e)

   

Часть 1. Сканирование виртуальной машины на windows10 без файрвола

1. Сканируем локальную сеть
 
   ip adress
   
   ![изображение](https://github.com/user-attachments/assets/b4efcfd6-c678-4af1-aa1b-3e4ee576b78e)

   netdiscover -r 192.168.1.0/24
   
   ![изображение](https://github.com/user-attachments/assets/2e5e2e9d-d0e8-4e04-8334-2e3382266336)

   Обнаружили вируальную машину
   
3. Используем nmap для обнаружения открытых портов, версии ОС
 
   nmap -A -sV -oN nmapscan.txt 192.168.1.41
   
   ![изображение](https://github.com/user-attachments/assets/42dab8ff-6ff5-439b-b63f-e793265275e2)

   nmap узнал открытые порты и версию ОС
   
4. Используем nmap в сочетании со скриптом vulners для проверки на уязвимости
 
   nmap -A -sV -oN nmapscanvulners.txt --script vulners 192.168.1.41

   ![изображение](https://github.com/user-attachments/assets/7f514cd4-36f8-4832-884e-709bce07b1a2)

   nmap не выявил уязвимостей :c
    

5. Сканер уязвимостей Сканер-ВС 6

![изображение](https://github.com/user-attachments/assets/3bfdd09f-3499-4601-853d-bb09ca6c4908)


![изображение](https://github.com/user-attachments/assets/7a9d4b8e-bea7-43a4-a9d9-a3751f3596cd)


![изображение](https://github.com/user-attachments/assets/1a7aaf8e-de22-43a7-8bed-19f62f82d7cf)



![изображение](https://github.com/user-attachments/assets/9765f4b8-6496-47ca-bf01-93240ef7d50d)



 
   Сканирование портов
   
  ![изображение](https://github.com/user-attachments/assets/71c2beb0-9cf2-4431-88f5-f473d209cf0c)

  Сканирование на уязвимости
  
  ![изображение](https://github.com/user-attachments/assets/5f132123-38f9-40bb-8647-a865bb7fb13c)

 
  ![изображение](https://github.com/user-attachments/assets/385ffec2-aee3-4acd-b3be-cdf80c07835d)

  ![изображение](https://github.com/user-attachments/assets/ea2488b0-5d99-4074-ac01-aa29355b1cca)

Уязвимость в протоколе HTTP/2
CVE-2023-44487
Уязвимость заключается в обработке мультиплексированных потоков в протоколе HTTP/2. Клиент может многократно запрашивать новый мультиплексный поток и сразу отправлять фрейм RST_STREAM для его отмены. Это создает дополнительные затраты для сервера на установление и закрытие потоков, при этом не достигая лимита сервера по максимальному количеству активных потоков на соединение, что приводит к отказу в обслуживании из-за потребления ресурсов сервера. Атаки могут осуществляться сравнительно небольшими ботнетами, состоящими примерно из 20 000 устройств.

Эксплуатация:
Уязвимость позволяет удаленному злоумышленнику вызвать отказ в обслуживании.

6. Сканер уязвимостей Nessus


![изображение](https://github.com/user-attachments/assets/9058884c-efd1-49a9-93ac-67f73e386db8)


![изображение](https://github.com/user-attachments/assets/b52e8772-0b72-45ce-8fd6-16cbb903d017)


![изображение](https://github.com/user-attachments/assets/15762765-851f-457e-98a8-6825e3f3c5c7)






![изображение](https://github.com/user-attachments/assets/6c7f28a7-65cc-425a-8c95-f40f39cff102)

![изображение](https://github.com/user-attachments/assets/58e6ae1d-7c76-43cd-af74-389d3fe38cf7)


![изображение](https://github.com/user-attachments/assets/f99e7d8f-e52a-4578-855c-a10ae3737a2a)

Подпись SMB не требуется
Описание
Подписание на удаленном SMB-сервере не требуется. Удаленный злоумышленник, не прошедший проверку подлинности, может использовать это для проведения атак «человек посередине» на SMB-сервер.
Решение
Обеспечьте подписание сообщений в конфигурации хоста. В Windows это можно найти в параметре политики «Сетевой сервер Microsoft: использовать цифровую подпись (всегда)». В Samba этот параметр называется «подпись сервера». Дополнительную информацию см. по ссылкам «см. также».



![изображение](https://github.com/user-attachments/assets/9e5d3d45-e264-4762-9cf8-4827c0ffcc70)

Запрос метки времени ICMP Удаленное раскрытие даты
Описание
Удаленный хост отвечает на запрос метки времени ICMP. Это позволяет злоумышленнику узнать дату, установленную на целевой машине, что может помочь удаленному злоумышленнику, не прошедшему аутентификацию, обойти протоколы аутентификации, основанные на времени.

Временные метки, возвращаемые с компьютеров под управлением Windows Vista/7/2008/2008 R2, намеренно неверны, но обычно они отстают от фактического системного времени в пределах 1000 секунд.
Решение
Отфильтруйте запросы меток времени ICMP (13) и исходящие ответы меток времени ICMP (14).


![изображение](https://github.com/user-attachments/assets/eed43b7a-e564-4680-b687-3eecb8e2a135)

Этот плагин представляет собой «полуоткрытый» сканер портов SYN. Он должен быть достаточно быстрым даже против цели, защищенной брандмауэром.

Обратите внимание, что сканирование SYN менее интрузивно, чем сканирование TCP (полное подключение) в отношении сломанных служб, но оно может вызвать проблемы для менее надежных межсетевых экранов, а также оставить незакрытые соединения на удаленной цели, если сеть загружена.
Решение
Защитите свою цель с помощью IP-фильтра.



Часть 2. Установка и настройка файрвола Tinywall

Tinywall автоматически переводит все порты в режим невидимки для того, чтобы скрыть их от внешних атак
Имеет 5 режимов работы: обычная защита, разрешить исходящие соединения, блокировать все, отключить фаервол и режим обучения
Тестирование будем проводить в режиме обычная защита

![image](https://github.com/user-attachments/assets/c70d91fe-19cd-4665-8d70-bf974b291f9e)


![image](https://github.com/user-attachments/assets/5a4b3e7f-360e-4f57-a162-febfa358b453)


![image](https://github.com/user-attachments/assets/5ffe741f-fba6-4654-8f93-aad551e285e7)

![image](https://github.com/user-attachments/assets/f3934789-c65f-4fe3-8af6-a4d23507fc9f)

Проверим, действительно ли Tinywall ограничивает доступ в интернет приложениям, не находящимся в белом списке
Воспользуемся небольшой программой 2ip Firewall Tester

![image](https://github.com/user-attachments/assets/23795a2e-95bf-4822-b8bb-ccdb741d547b)

Tinywall проходит тест


Часть 3. Сканирование виртуальной машины на windows10 с включенным файрволом tinywall

1.

  ip adress
   
   ![изображение](https://github.com/user-attachments/assets/9ad49f83-1b5d-42a5-8cdc-bd8f31738d90)


   netdiscover -r 192.168.1.0/24 

   ![изображение](https://github.com/user-attachments/assets/4d040d1e-3f7a-4e5f-aec1-b60803307a98)


2.

   nmap -A -sV 192.168.1.41 


   ![изображение](https://github.com/user-attachments/assets/528028f9-469a-4ea0-aa27-5f642ebc2841)

   nmap не обнаружил открытые порты

4. 

    nmap -A -sV --script vulners 192.168.1.41

   
   ![изображение](https://github.com/user-attachments/assets/1b76bff0-8a5f-4808-b245-e2bc478ebe76)


6.

   Сканер-ВС 6
   
   ![изображение](https://github.com/user-attachments/assets/c68dbe13-1e2b-4e92-acac-52d9ef2b44b3)

   не получил никаких данных, сканирование на уязвимости невозможно

   
7.
   
   Сканер Nessus

   ![изображение](https://github.com/user-attachments/assets/51d47f7b-ecba-4a0b-bba4-d95d4fdb8fbb)

   ![изображение](https://github.com/user-attachments/assets/faacd5f9-cd63-40b0-a499-e87134aa0348)

   не обнаружил уязвимостей
