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

