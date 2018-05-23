# solomon585858_microservices
solomon585858 microservices repository


## ДЗ 13. Docker 1

 - [x] Основное ДЗ
 - [x] Задание со *

#### В процессе сделано:
 - Были установлены **Docker**, **docker-machine**, **docker-compose**
 - Был создан и запущен тестовый контейнер **hello-world**
 - Был создан и запущен контейнер из образа **ubuntu**
 - Был создан образ из контейнера
 - В файл **docker-monolith/docker-1.log** записан вывод команды **docker images**
 - В рамках задания со * в файл **docker-monolith/docker-1.log** были записаны отличия вывода команды **docker inspect** для образа и контейнера


#### Как запустить проект:
 - Для создания и запуска контейнера использовать команду **docker run**
 - Для создания образа из контейнера использовать команду **docker commit**

#### Как проверить работоспособность:
 - Список запущенных контейнеров можно посмотреть с помощью команды **docker ps**
 - Список всех контейнеров можно посмотреть с помощью команды **docker ps -a**
 - Список сохраненных образов можно посмотреть с помощью команды **docker images**
 
#### PR checklist
 - [x] Выставил label **Homework-13** с номером домашнего задания
 - [x] Выставил label **docker** с номером домашнего задания


## ДЗ 14. Docker 2

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Был создан новый проект **docker** в GCE
 - Был создан **docker-host** в GCE с помощью **docker-machine**
 - Был повторен список тестов из демо по **PID namespace**, **net namespace**, **user namespaces**
 - Был создан образ **reddit** с тэгом **latest** на базе **Dockerfile**
 - Было добавлено правило в firewall GCE, разрешающее входящий TCP-трафик на порт 9292
 - Был развернут docker контейнер на базе созданного образа
 - Зарегистрировался на **Docker Hub** под учетной записью **solomon5858558**
 - Был загружен созданный образ на **Docker Hub** и запущен впоследствии локально

#### Как запустить проект:
 - Для создания docker образа использовать команду **docker build -t reddit:latest**
 - Для добавления правила в firewall GCE использовать команду **gcloud compute firewall-rules create reddit-app --allow tcp:9292 --target-tags=docker-machine -description="Allow PUMA connections" --direction=INGRESS**
 - Для загрузки docker образа на **Docker Hub** использовать команды **docker tag reddit:latest solomon58585558/otus-reddit:1.0** и **docker push solomon58585558/otus-reddit:1.0**
 - Для запуска docker контейнера в локальном docker использовать команду **docker run --name reddit -d -p 9292:9292 solomon5858558/otus-reddit:1.0**

#### Как проверить работоспособность:
 - Приложение должно быть доступно по адресу **http://IPaddrofapplication:9292**
 
#### PR checklist
 - [x] Выставил label **Homework-14** с номером домашнего задания
 - [x] Выставил label **docker** с номером домашнего задания


## ДЗ 15. Docker 3

 - [x] Основное ДЗ
 - [x] Задание со *

#### В процессе сделано:
 - Был установлен **linter** для работы с **docker** образами
 - Были добавлены компоненты приложения (**post-py**, **comment**, **ui** в каталог **src** репозитория)
 - Были созданы **Dockerfile**-ы для **post-py**, **comment**, **ui** и подкорректированы с учетом **linter**
 - Были собраны образы для **post-py**, **comment**, **ui**
 - Была создана bridge-сеть **reddit** и запущены контейнеры с алиасами, подключенные к этой сети
 - Был пересобран образ для **ui** версии 2.0 для уменьшения занимаего места
 - Был создан **volume** с названием **reddit_db** и подключен к mongodb
 - В задании со * для контейнеры для сервисов были запущены с другими сетевыми алиасами и с указанием адресов для взаимодействия через ENV-переменные
 - В задании со * был собран образ для **ui** на базе **Alpine Linux**

#### Как запустить проект:
 - Для проверки **linter**-ом **Dockerfile**-а использовать команду **hadolint Dockerfile**
 - Для создания сети для приложения использовать команду **docker network create reddit**
 - Для создания контейнеров с сервисами использовать команды **docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db mongo:latest**, **docker run -d --network=reddit --network-alias=post solomon5858558/post:1.0**, **docker run -d --network=reddit --network-alias=comment solomon5858558/comment:1.0**, **docker run -d --network=reddit -p 9292:9292 solomon5858558/ui:1.0**
 - Для создания **volume** использовать команду **docker volume create reddit_db**
 - Для создания контейнеров с сервисами при покдлюченном **volume** использовать команды **docker run -d --network=reddit --network-alias=post_db --network-alias=comment_db -v reddit_db:/data/db mongo:latest**, **docker run -d --network=reddit --network-alias=post solomon5858558/post:1.0**, **docker run -d --network=reddit --network-alias=comment solomon5858558/comment:1.0**, **docker run -d --network=reddit -p 9292:9292 solomon5858558/ui:2.0**
 - В задании со * для содания контейнеров с другими сетевыми алиасами и с указанием адресов для взаимодействия через ENV-переменные использовать команды **docker run -d --network=reddit --network-alias=post_db_new --network-alias=comment_db_new mongo:latest**, **docker run -d -e "POST_DATABASE_HOST=post_db_new" --network=reddit --network-alias=post_new solomon5858558/post:1.0**, **docker run -d -e "COMMENT_DATABASE_HOST=comment_db_new" --network=reddit --network-alias=comment_new solomon5858558/comment:1.0**, **docker run -d -e "POST_SERVICE_HOST=post_new" -e "COMMENT_SERVICE_HOST=comment_new" --network=reddit -p 9292:9292 solomon5858558/ui:1.0**
 - В задании со * для создания образа на базе **Alpine Linux** для **ui** использовать команду **docker build -t solomon5858558/ui:3.0 ./ui**
 - Для просмотра созданных образов использовать команду **docker images** (в итоге для **ui** 1.0 - 766 MB, 2.0 - 399 MB, 3.0 - 238 MB)

#### Как проверить работоспособность:
 - Приложение должно быть доступно по адресу **http://IPaddrofapplication:9292**
 
#### PR checklist
 - [x] Выставил label **Homework-15** с номером домашнего задания
 - [x] Выставил label **docker** с номером домашнего задания


## ДЗ 16. Docker 4

 - [x] Основное ДЗ
 - [x] Задание со *

#### В процессе сделано:
 - Был установлен **docker compose**
 - Было протестирование создание контейнеров с **none**, **host**, **bridge** сетями
 - Было протестировано создание **bridge** сетей **back_net**, **front_net**
 - Было протестирование создание контейнеров с подключением к сетям **back_net**, **front_net**
процесс **docker-proxy**, который слушает сетевой tcp порт 9292
 - Был протестирован запуск приложения с помощью **docker-compose** на базе файла **docker-compose.yml**
 - Был отредактирован файл **docker-compose.yml** под кейс с множеством сетей, сетевых алиасов. Также были параметризированы с помощью переменных окружения порт публикации сервиса ui, версии сервисов, имя пользователя. Все переменные были описаные в файле **.env**. Сам файл был добавлен в **.gitignore**. Для примера был создан файл **.env.example**
 - В задании со * был протестирован запуск контейнеров с использованием драйверов none и host и просмотрен список namespace-ов
 - В задании со * были просмотрены **veth** интерфейсы для **bridge** интерфейсов созданных сетей и правила **iptables**, отвечающие за выпуск во внешнюю сеть контейнеров из **bridge** сетей, а также запущенный 
 - В задании со * был рассмотрен вопрос образования имени проекта. При создании контейнеров название контейнера начинается с названия проекта. По умолчанию название проекта соответствует названию базовой директории проекта. Для смены названия проекта можно воспользоваться либо параметром **-p** либо с помощью переменной **COMPOSE_PROJECT_NAME**.

#### Как запустить проект:
 - Для создания контейнера с сетью **none** можно воспользоваться командой **docker run --network none --rm -d --name net_test joffotron/docker-net-tools -c "sleep 100"**
 - Для создания контейнера с сетью **host** можно воспользоваться командой **docker run --network host --rm -d --name net_test joffotron/docker-net-tools -c "sleep 100"**
 - Для создания сетей **back_net**, **front_end** можно воспользоваться командами **docker network create back_net --subnet=10.0.2.0/24**, **docker network create front_net --subnet=10.0.1.0/24**
 - Для подключения контейнеров **post**, **comment** к сети **front_net** можно воспользоваться командами **docker network connect front_net post**, **docker network connect front_net comment**
 - Для запуска приложения с помощью **docker-compose** можно воспользоваться командой **docker-compose up**

#### Как проверить работоспособность:
 - Приложение должно быть доступно по адресу **http://IPaddrofapplication:9292**
 
#### PR checklist
 - [x] Выставил label **Homework-16** с номером домашнего задания
 - [x] Выставил label **docker** с номером домашнего задания


 ## ДЗ 17. GitlabCI 1

 - [x] Основное ДЗ
 - [x] Задание со *

#### В процессе сделано:
 - Была создана виртуальная машина для **Gitlab CI**
 - Был установлен **Gitlab CI** с помощью **Omnibus**
 - Были созданы **Group**, **Project**, **CI/CD Pipeline**
 - Был зарегистрирован и запущен **Runner**
 - Был добавлен файл **.gitlab-ci.yml**
 - Был добавлен исходный код **reddit** в репозиторий
 - Было протестировано приложение **reddit**
 - Была настроена интеграция **Gitlab CI** со **Slack-ом**

#### Как запустить проект:
 - Для установки **docker** необходимо выполнить команды **curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -**, **add-apt-repository "deb https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"**, **apt-get update && apt-get install docker-ce docker-compose**
 - Для подготовки окружения необходимо выполнить команды **mkdir -p /srv/gitlab/config /srv/gitlab/data /srv/gitlab/logs**, **cd /srv/gitlab/**, **touch docker-compose.yml**
 - Для запуска Gitlab CI необходимо выполнить команду **docker-compose up -d**

#### Как проверить работоспособность:
 - Gitlab CI должен быть доступен по адресу **http://IPAddressOFGitlabCI/**
 - При каждом изменении в коде приложения должен быть запущен тест и информация должна быть отражена в Slack-чате
 
#### PR checklist
 - [x] Выставил label **Homework-17** с номером домашнего задания
 - [x] Выставил label **GitlabCI** с номером домашнего задания


 ## ДЗ 18. GitlabCI 2

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Была создан проект **example2**
 - Был включен **runner** для нового проекта
 - Было описано окружение **dev**
 - Были описаны окружения **stage**, **production**
 - Была добавлена директива **only** в описание **pipeline**, которая не позволит выкатить код на **stage**, **production** без тэга
 - Было настроено динамическое окружение для каждой ветки в репозитории кроме ветки master
 - Была настроена интеграция **Gitlab CI** со **Slack-ом**

#### Как запустить проект:
 - Для запуска **pipeline** с учетом изменения, помеченного тэгом, нужно выполнить команду **git push gitlab2 gitlab-ci-2 --tags**

#### Как проверить работоспособность:
 - Gitlab CI должен быть доступен по адресу **http://IPAddressOFGitlabCI/**
 
#### PR checklist
 - [x] Выставил label **Homework-18** с номером домашнего задания
 - [x] Выставил label **GitlabCI** с номером домашнего задания


