# Лабораторная работа IWNO4: Использование контейнеров как среды выполнения

## Цель работы
Данная лабораторная работа призвана напомнить основные команды ОС Debian/Ubuntu. Также она позволит познакомиться с Docker и его основными командами.

## Задание
Запустить контейнер Ubuntu, установить Web-сервер Apache и вывести в браузере страницу с текстом "Hello, World!".

## Выполнение

Создаём репощиторий containers03, клонируем и отрываем терминал в этом каталоге

Запускаем DockerDesktop т.к с ним запустится и сам инструмент Docker

Выполняем команду:
```docker run -ti -p 8000:80 --name containers03 ubuntu bash```

    docker run - запускает контейнер

    -ti - комбинация двух флагов (-t и -i), которая запускает псевдотерминал для взаимодействия с контейнером

    -p - флаг для маппинга порта 8000:80 (Мы мыпим внутренний порт контейнера 80 на внешний порт 8000) (В дальнейшем мне придётся перемапить порт на 8080 т.к 8000 занят на моём компьютере)

    --name containers03 - задаёт имя контейнера

    ubuntu bash - указывает что в качестве образа мы используем образ ubuntu и запускаем bash, с которой будем взаимодействовать через терминал, заданный флагом -ti

![Alt text](/images/Снимок%20экрана%202025-02-28%20115805.png "image")

После выполнения команды открывается терминал bash.

Вписываем команды:

```bash
    apt update - обновление списков репозиториев

    apt install apache2 -y - установка apache2 сфлагом -y для последующей установки

    service apache2 start - запуск apache2
```

![Alt text](/images/Снимок%20экрана%202025-02-28%20115847.png "image")
![Alt text](/images/Снимок%20экрана%202025-02-28%20115908.png "image")
![Alt text](/images/Снимок%20экрана%202025-02-28%20120021.png "image")

Тут я получил BadRequest из за которого пришлось перемапить порты т.к 8000 был занят другим сервисом

![Alt text](/images/Снимок%20экрана%202025-02-28%20120039.png "image")

Открываем http://localhost:8080 и видим страницу

![Alt text](/images/Снимок%20экрана%202025-02-28%20122856.png "image")

Вписываем в терминал команды:

```bash
    ls -l /var/www/html/ - выводим содержимое директории в терминал

    echo '<h1>Hello, World!</h1>' > /var/www/html/index.html - в файл index.html добавляем строку <h1>Hello, World!</h1>
```

![Alt text](/images/Снимок%20экрана%202025-02-28%20120237.png "image")

Обновляем страницу и видим Hello World

![Alt text](/images/Снимок%20экрана%202025-02-28%20122953.png "image")

Выполняем команды:

```bash
    cd /etc/apache2/sites-enabled/ - переход в директорию sites-enabled
    cat 000-default.conf - вывод в терминал содержимого файла000-default.conf
```

![Alt text](/images/Снимок%20экрана%202025-02-28%20120835.png "image")

Данный файл содержит настройки нашего веб сервера

Командой ```exit``` выходим и вводим ```docker ps -a``` чтобы получить список всех контейнеров

![Alt text](/images/Снимок%20экрана%202025-02-28%20121345.png "image")

Видим наш контейнер ubuntu и удаляем его командой ```docker rm containers03```

![Alt text](/images/Снимок%20экрана%202025-02-28%20121356.png "image")

## Выводы 

Мы сумели запустить докер контейнер при помощи терминала и настроить внутри контейнера веб сервер, до которого достучались при помощи браузера по localhost. С непосредственным содержимым контейнера мы взаимодействовали через терминал и стандартную систему ввода/вывода у контейнеров