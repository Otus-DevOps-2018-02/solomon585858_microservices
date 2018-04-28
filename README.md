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
