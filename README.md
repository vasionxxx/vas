# Оркестрация группой Docker контейнеров на примере Docker Compose. Бодарев В.В.

# Задача 1
https://hub.docker.com/repository/docker/vasionx/nginx-custom/general

# Задача 2

Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:

имя контейнера "ФИО-custom-nginx-t2"

контейнер работает в фоне

контейнер опубликован на порту хост системы 127.0.0.1:8080

![image alt](https://github.com/vasionxxx/vas/blob/main/21.png)

Не удаляя, переименуйте контейнер в "custom-nginx-t2"

![image alt](https://github.com/vasionxxx/vas/blob/main/22.png)

Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html

![image alt](https://github.com/vasionxxx/vas/blob/main/23.png)

Убедитесь с помощью curl или веб браузера, что индекс-страница доступна

![image alt](https://github.com/vasionxxx/vas/blob/main/24.png)

# Задача 3

Подключитесь к контейнеру и нажмите комбинацию Ctrl-C

![image alt](https://github.com/vasionxxx/vas/blob/main/31.png)

Причина остановки связана с тем что мы нажали Ctrl-C, что отправило сигнал SIGINT и завершило выполнение основного процесса контейнера

![image alt](https://github.com/vasionxxx/vas/blob/main/32.png)

Перезапустите контейнер

![image alt](https://github.com/vasionxxx/vas/blob/main/33.png)

Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash

![image alt](https://github.com/vasionxxx/vas/blob/main/34.png)

Установим nano

![image alt](https://github.com/vasionxxx/vas/blob/main/35.png)

Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81"

![image alt](https://github.com/vasionxxx/vas/blob/main/36.png)

Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81

![image alt](https://github.com/vasionxxx/vas/blob/main/37.png)

![image alt](https://github.com/vasionxxx/vas/blob/main/38.png)

Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.

Проблема связана с неправильным пробросом портов или тем, что контейнер не слушает нужные порты. 

![image alt](https://github.com/vasionxxx/vas/blob/main/39.png)

Удалите запущенный контейнер "custom-nginx-t2", не останавливая его

![image alt](https://github.com/vasionxxx/vas/blob/main/399.png)

# Задача 4

Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v

![image alt](https://github.com/vasionxxx/vas/blob/main/41.png)

Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера

![image alt](https://github.com/vasionxxx/vas/blob/main/42.png)

Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data

![image alt](https://github.com/vasionxxx/vas/blob/main/43.png)

Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине

![image alt](https://github.com/vasionxxx/vas/blob/main/44.png)

Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера

![image alt](https://github.com/vasionxxx/vas/blob/main/45.png)

# Задача 5

Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. Выполните команду "docker compose up -d". Какой из файлов был запущен и почему?

Путь по умолчанию для файла Compose — compose.yaml. Compose также поддерживает docker-compose.yaml для обратной совместимости с более ранними версиями. Если существуют оба файла, Compose предпочитает compose.yaml. 

![image alt](https://github.com/vasionxxx/vas/blob/main/51.png)

Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла

![image alt](https://github.com/vasionxxx/vas/blob/main/52.png)

Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry

![image alt](https://github.com/vasionxxx/vas/blob/main/53.png)

![image alt](https://github.com/vasionxxx/vas/blob/main/54.png)

Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз

![image alt](https://github.com/vasionxxx/vas/blob/main/55.png)

![image alt](https://github.com/vasionxxx/vas/blob/main/56.png)

Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver"

![image alt](https://github.com/vasionxxx/vas/blob/main/57.png)

Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения. 

Получим предупреждение, что docker compose не может найти файл compose.yaml, так как он был удален. В данном случае docker compose будет использовать только оставшийся файл docker-compose.yaml, который, возможно, не содержит все необходимые сервисы. 

![image alt](https://github.com/vasionxxx/vas/blob/main/58.png)

Выполните предложенное действие

![image alt](https://github.com/vasionxxx/vas/blob/main/59.png)

Погасите compose-проект ОДНОЙ(обязательно!!) командой.

![image alt](https://github.com/vasionxxx/vas/blob/main/599.png)
