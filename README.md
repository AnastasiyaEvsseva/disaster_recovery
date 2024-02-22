# disaster_recovery

### Задание 1
1. Дана схема для Cisco Packet Tracer, рассматриваемая в лекции.
2. На данной схеме уже настроено отслеживание интерфейсов маршрутизаторов Gi0/1 (для нулевой группы)
3. Необходимо аналогично настроить отслеживание состояния интерфейсов Gi0/0 (для первой группы).
4. Для проверки корректности настройки, разорвите один из кабелей между одним из маршрутизаторов и Switch0 и запустите ping между PC0 и Server0.
5. На проверку отправьте получившуюся схему в формате pkt и скриншот, где виден процесс настройки маршрутизатора.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/52f638da-ffe3-4f4c-99a4-deca9ebad8db)

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/72b36d19-d708-4884-819a-92eb1aea763d)

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/ce736582-4dbb-4643-a33c-9ed3bfa2d511)

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/0b887f0e-690a-4a9d-92f3-ecc977802a54)

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/3550c028-d273-4e7f-8b3b-8b9f7403c4d5)

### Задание 2
1. Запустите две виртуальные машины Linux, установите и настройте сервис Keepalived как в лекции, используя пример конфигурационного файла.
2. Настройте любой веб-сервер (например, nginx или simple python server) на двух виртуальных машинах
3. Напишите Bash-скрипт, который будет проверять доступность порта данного веб-сервера и существование файла index.html в root-директории данного веб-сервера.
4. Настройте Keepalived так, чтобы он запускал данный скрипт каждые 3 секунды и переносил виртуальный IP на другой сервер, если bash-скрипт завершался с кодом, отличным от нуля (то есть порт веб-сервера был недоступен или отсутствовал index.html). Используйте для этого секцию vrrp_script
5. На проверку отправьте получившейся bash-скрипт и конфигурационный файл keepalived, а также скриншот с демонстрацией переезда плавающего ip на другой сервер в случае недоступности порта или файла index.html

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/be440bc8-6f77-49a9-ae5c-1fb26d888589)

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/05496eb8-6769-428d-a5d2-089255bc5b3f)

Содержание конфига мастер-сервера.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/4a5ba33b-920a-47cf-ad56-f66d0b8bfe53)

Содержание конфига бекап-сервера. Как видно, значения state и priority отличаются.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/e680d0cc-5806-477c-a27c-28f472165578)

Как видно, скрипт работает. В обычных условиях Keepalive находится в состоянии MASTER

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/e5df1ed3-c815-4914-839b-84a5f311a54f)

При обращении по виртуальному IP адресу, он направляет нас на страницу мастер-сервера.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/59160ba1-8996-4eef-93ff-d10bd9bec2be)

Сымитируем падение сервиса nginx на мастер-сервере и снова обратимся по виртуальному IP адресу.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/6e020c9b-c0cc-4eee-984f-165ce52d03eb)

Теперь он направил нас на страницу бекап-сервера, т.к. порт 80 на мастер-сервере недоступен после остановки работы nginx. Keepalive отработал в соответствии с написанным скриптом.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/0b6e66a9-d5a9-4dfe-8585-e92a8c6be48f)

Проверим, что при возвращении нормальных условий виртуальный IP адрес снова будет направлять на основной сервер.

![image](https://github.com/AnastasiyaEvsseva/disaster_recovery/assets/151757353/01378997-0b04-4a98-a124-82908ea2df02)













   










   
