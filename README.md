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


 ## ДЗ 19. Monitoring 1

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Было создано окружение для развертывания **Prometheus**
 - Была создана директория **docker** в корне репозитория и перенесены в нее директория **docker-monolith** и файлы **docker-compose** и все **env**
 - Была создана директория **monitoring**, в которой будут хранится все файлы, касающиеся мониторинга
 - Были собраны **Docker** образы и запушены в **Docker Hub**: **solomon5858558/ui** (*https://hub.docker.com/r/solomon5858558/ui/*), **solomon5858558/comment** (*https://hub.docker.com/r/solomon5858558/comment/*), **solomon5858558/post** (*https://hub.docker.com/r/solomon5858558/post/*), **solomon5858558/prometheus** (*https://hub.docker.com/r/solomon5858558/prometheus/*)
 - Был развернут **Prometheus** совместно с микросервисами в **Docker** контейнере с помощью **docker-compose.yml**
 - Были просмотрены **targets**, **endpoints**, **healthchecks**, **metrics**, **graphs** в GUI
 - Была протестирована остановка **post**, **comment** сервисов
 - Была протестирована сборка метрик хоста с помощью **Node exporter**

#### Как запустить проект:
 - Для сбора **Docker** для **Prometheus** нужно выполнить команду **docker build -t $USER_NAME/prometheus .**
 - Для развертывания **Prometheus** совместно с микросервисами в **Docker** контейнере нужно выполнить команду **docker-compose up -d**

#### Как проверить работоспособность:
 - **Prometheus** должен быть доступен по адресу **http://IPAddressOFPrometheus:9292/graph**
 
#### PR checklist
 - [x] Выставил label **Homework-19** с номером домашнего задания
 - [x] Выставил label **Monitoring** с номером домашнего задания


 ## ДЗ 20. Monitoring 2

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Были развернуты микросервисы и **Prometheus**, **cAdvisor**, **Grafana**, **Alertmanager** в **Docker** контейнерах
 - Были собраны **Docker** образы и запушены в **Docker Hub**: **solomon5858558/ui** (*https://hub.docker.com/r/solomon5858558/ui/*), **solomon5858558/comment** (*https://hub.docker.com/r/solomon5858558/comment/*), **solomon5858558/post** (*https://hub.docker.com/r/solomon5858558/post/*), **solomon5858558/prometheus** (*https://hub.docker.com/r/solomon5858558/prometheus/*), **solomon5858558/alertmanager** (*https://hub.docker.com/r/solomon5858558/alertmanager/*)
 - Файл **docker-compose.yml** был разбит на два файла - **docker-compose.yml** и **docker-compose-monitoring.yml**
 - Был равзернут **cAdvisor** для мониторинга состояния контейнеров
 - Была развернута **Grafana** и добавлены **Dashboards**, метрики мониторинга приложения и бизнес-метрики
 - Был развернут **Alertmanager** и протестированы алерты в **Slack**

#### Как запустить проект:
 - Для развертывания **Prometheus**, **cAdvisor**, **Grafana**, **Alertmanager** в **Docker** контейнерах нужно выполнить команду **docker-compose -f docker-compose-monitoring.yml up -d**
 - Для развертывания микросервисов в **Docker** контейнерах нужно выполнить команду **docker-compose up -d**

#### Как проверить работоспособность:
 - **Prometheus** должен быть доступен по адресу **http://IPAddressOFPrometheus:9292/graph**
 - **cAdvisor** должен быть доступен по адресу **http://IPAddressOFcAdvisor:8080/containers**
 - **Grafana** должен быть доступен по адресу **http://IPAddressOFGrafana:3000**
 - **Alertmanager** должен быть доступен по адресу **http://IPAddressOFAlertmanager:9093**
 
#### PR checklist
 - [x] Выставил label **Homework-20** с номером домашнего задания
 - [x] Выставил label **Monitoring** с номером домашнего задания


 ## ДЗ 21. Logging 1

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Были развернуты **ElasticSearch**, **Fluentd**, **Kibana** в **Docker** контейнерах
 - Были рассмотрены структурированные логи на примере сервиса **post**
 - Были рассмотрены неструктурированные логи на примере сервиса **ui**
 - Была развернута система распределенного трейсинга **Zipkin** в **Docker** контейнере

#### Как запустить проект:
 - Для развертывания сервисов использовать команду **docker-compose -f docker-compose-logging.yml -f docker-compose.yml up -d**

#### Как проверить работоспособность:
 - **Kibana** должен быть доступен по адресу **http://IPAddressOFKibana:5601**
 - **Zipkin** должен быть доступен по адресу **http://IPAddressOFcZipkin:9411**
 
#### PR checklist
 - [x] Выставил label **Homework-21** с номером домашнего задания
 - [x] Выставил label **Logging** с номером домашнего задания


 ## ДЗ 22. Kubernetes 1

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Был развернут **Kubernetes-кластер** и все его компоненты **The Hard Way** на базе руководства от *Kelsey Hightower-а*
 - Были развернуты тестовые **Pods** на базе созданных **deployment-ов**
 - Был удален тестовый **Kubernetes-кластер** после выполнения всех тестов

#### Как запустить проект:
 - Для развертывания **mongo** на базе **deployment** файла использовать команду **kubectl apply -f mongo-deployment.yml**
 - Для развертывания **comment** на базе **deployment** файла использовать команду **kubectl apply -f comment-deployment.yml**
 - Для развертывания **post** на базе **deployment** файла использовать команду **kubectl apply -f post-deployment.yml**
 - Для развертывания **ui** на базе **deployment** файла использовать команду **kubectl apply -f ui-deployment.yml**

#### Как проверить работоспособность:
 - Список созданных **Pods** можно посмотреть с помощью команды **kubectl get pods -o wide**
 - Список созданных **Deployments** можно посмотреть с помощью команды **kubectl get deployments -o wide**
 
#### PR checklist
 - [x] Выставил label **Homework-22** с номером домашнего задания
 - [x] Выставил label **Kubernetes** с номером домашнего задания


 ## ДЗ 23. Kubernetes 2

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Было развернуто локальное окружение для работы с **Kubernetes**
 - Был развернут **Kubernetes** в **GKE**
 - Был запущен сервис **reddit** в **Kubernetes**

#### Как запустить проект:
 - Для запуска **Minikube** кластера использовать команду **minikube start**
 - Для подключения к **Kubernetes** в **GKE** использовать команду **gcloud container clusters get-credentials cluster-1 --zone us-west1-b --project docker-201804**
 - Для создания **dev namespace** использовать команду **kubectl apply -f ./kubernetes/reddit/dev-namespace.yml**
 - Для запуска сервиса **reddit** в **dev namespace** использовать команду **kubectl apply -f ./kubernetes/reddit/ -n dev**
 - Для назначения роли **cluster-admin** для **Service Account** с именем **kube-system:kubernetes-dashboard** использовать команду **kubectl create clusterrolebinding kubernetes-dashboard  --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard**
 - Для подключение к **Kubernetes Dashboard** использовать команды **kubectl proxy** и **http://localhost:8001/ui**

#### Как проверить работоспособность:
 - Список созданных **Pods** можно посмотреть с помощью команды **kubectl get pods -o wide -n dev**
 - Список созданных **Deployments** можно посмотреть с помощью команды **kubectl get deployments -o wide -n dev**
 - Веб-интерфейс приложения **reddit** должен быть доступен по ссылке **http://node-ip:NodePort**. В нашем случае это **http://35.227.155.158:32092/**. Скриншот выложен в виде файла **kubernetes/reddit/UI_SCREENSHOT.png**
 
#### PR checklist
 - [x] Выставил label **Homework-23** с номером домашнего задания
 - [x] Выставил label **Kubernetes** с номером домашнего задания


 ## ДЗ 24. Kubernetes 3

 - [x] Основное ДЗ
 - [x] Задание со *

#### В процессе сделано:
 - Была протестирована работа с **Ingress Controller**, **Ingress**, **Secret**, **TLS**, **LoadBalancer Service**, **Network Policies**, **PersistentVolumes**, **PersistentVolumeClaims**
 - В задании со * объект **Secret** был описан с помощью **Kubernetes** манифеста (файл **ui-secret.yml**). В рамках **ui-secret.yml** были добавлены **tls.key** и **tls.crt** в **base64** т.к. **Kubernetes** хранит эти файлы в **base64**

#### Как запустить проект:
 - Для создания **Secret** в **Namespace** с именем **dev** использовать команду **kubectl apply -f ui-secret.yml** (задание со *)
 - Для включения **Network Policy** для **GKE** использовать команды **gcloud beta container clusters update cluster-1 --zone=us-west1-b --update-addons=NetworkPolicy=ENABLED**, **gcloud beta container clusters update cluster-1 --zone=us-west1-b --enable-network-policy**
 - Для применения **Network Policy**, запрещающую входящий трафик для **mongodb** от всех **Pod**-ов кроме **comment** и **post** использовать команду **kubectl apply -f mongo-network-policy.yml -n dev**
 - Для создания диска в **Google Cloud** использовать команду **gcloud compute disks create --size=25GB --zone=us-west1-b reddit-mongo-disk**
 - Для монтирования выделенного диска к **Pod** с именем **mongo** использовать команду **kubectl apply -f mongo-deployment.yml -n dev**
 - Для добавления **PersistentVolume** в кластер использовать команду **kubectl apply -f mongo-volume.yml -n dev**
 - Для добавления **PersistentVolumeClaim** в кластер использовать команду **kubectl apply -f mongo-claim.yml -n dev**
 - Для добавления **StorageClass** в кластер использовать команду **kubectl apply -f storage-fast.yml -n dev**
 - Для добавления **PersistentVolumeClaim** в кластер использовать команду **kubectl apply -f mongo-claim-dynamic.yml -n dev**

#### Как проверить работоспособность:
 - Веб-интерфейс приложения **reddit** должен быть доступен по ссылке **https://35.186.253.127/**
 
#### PR checklist
 - [x] Выставил label **Homework-24** с номером домашнего задания
 - [x] Выставил label **Kubernetes** с номером домашнего задания


 ## ДЗ 25. Kubernetes 4

 - [x] Основное ДЗ
 - [ ] Задание со *

#### В процессе сделано:
 - Были установлены **Helm**, **Tiller**
 - Был развернут **Gitlab** в **Kubernetes**
 - Был протестирован запуск **CI/CD** конвейера 

#### Как запустить проект:
 - Для создания и запуска **Tiller** сервера использовать команды **kubectl apply -f tiller.yml** и **helm init --service-account tiller** 
 - Для обновления зависимости чарта **reddit** использовать команду **helm dep update ./reddit**
 - Для установки приложения использовать команду **helm install reddit --name reddit-test**
 - Для обновления релиза, установленного в k8s, использовать команду **helm upgrade reddit-test ./reddit** 
 - Добавить пул узлов **bigpool** в **GKE**
 - Включить **Устаревшие права доступа** в **GKE**
 - Для установки **Gitlab** выполнить команду **helm install --name gitlab . -f values.yaml**
 - Добавить группу **solomon5858558** и проекты **ui, post, comment, reddit-deploy**
 - Добавить 2 переменные **CI_REGISTRY_USER** (логин в **Docker Hub**), **CI_REGISTRY_PASSWORD** (пароль от **Docker Hub**) в **Gitlab**
 - Запушить код приложения в каждую ветку

#### Как проверить работоспособность:
 - Приложения должны быть доступны по ссылкам **http://staging**, **http://production**
 
#### PR checklist
 - [x] Выставил label **Homework-25** с номером домашнего задания
 - [x] Выставил label **Kubernetes** с номером домашнего задания