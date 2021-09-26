Образ размещен в открытом репозитории на Dockerhub
link https://hub.docker.com/repository/docker/vadimklm/lab1

Также все файлы для сборки залиты на GitHub 
link https://github.com/vadimklimenko/Docker

Выгружаем файлы с GitHub:
- docker-compose.yml
- Dockerfile
- index.html
- nginx.conf
- README.md
- targets.json

И размещаем их в папке с которой будем запускать образ.

Описание файлов:

docker-compose.yml

- Используем версию 3;
- В сервисах веб используем наш build, который собран в Dockerfile;
- Прописывем порты для работы;
- Монтируем файлы nginx.conf для настроек nginx и targets.json в директорию необходимую по задаче (/var/http);

Dockerfile
- Устанавливаем с DockerHub образ alpine OS версии 3.14;
- Обновляем все фалый системы и устанавливаем nginx и bash;
- Загружаем в корневую директорию вебсервера nginx файл index.html;
- Запускаем nginx на переднем плане (foreground);

nginx.conf
- Указаны основные настройки для nginx и правила работы endpoint /api/targets;

index.html
- Создвнный для удобства перехода по endpoint file, при необходимости его можно прописать руками в URL;

targets.json
- Файл требуемый по задаче, залиты тестовые данные;


Для запуска контейнера используем команду 
docker-compose up

После запуска по нашему хосту порт 8080 будет запущен файл index.html;
Далее переходим по enpoint /api/targets по ссылке в индексном файле или через url строку;
В результате сервер выводит содержимое файла targets.json расположенного внутри образа в директории /var/http;
Также мы можем подмонтировать данный файл из файловой системы host изменив содержание targets.json в папке, где запускали образ;
Изменения сразу будут отображены по enpoint /api/targets после его перезагрузки;



