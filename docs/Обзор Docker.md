# Обзор Docker
Docker это открытая платформа для разработки, поставки и запуска приложений. Он позволяет вам отделить ваши приложения от инфраструктуры, что ускоряет поставку программ. С Docker вы можете настраивать инфраструктуру таким же образом, что и приложения. Используя преимущества методик для быстрой поставки, тестирования и развертывания кода, вы можете значительно уменьшить задержку между написанием кода и его запуском на производственной среде.
## Платформа Docker
Docker дает возможность упаковать приложение со всеми зависимостями и запустить его в изолированной среде, называемой *контейнером*. Изоляция и защищенность позволяет запускать много контейнеров одновременно на одном хосте. Контейнеры легковесны и содержат все, что необходимо для запуска приложения, так что вам не нужно полагаться на то, что в данный момент уже установлено на хосте. Вы можете легко делиться контейнерами и быть уверенным, что все получают точно такой же контейнер, работающий тем же образом.

Docker предусматривает утилиты и платформу для управления циклом жизни ваших контейнеров:

 - Разработка приложения и поддержка его компонентов с помощью контейнеров.
 - Контейнер становится единицей для распределения и тестирования ваших приложений.
 - Когды все готово, разверните свое приложение в свою производственную среду как контейнер или оркестированный[^1] сервис. Это работает одинаково независимо от того, ваша производтвенная среда это локальный дата-центр, облачный поставщик или их смесь.
 
 [^1]: Оркестированние - автоматическая конфигурация, управление и координация компьютерных систем, приложений и сервисов.

## Для чего можно использовать Docker?
> Быстрая и последовательная поставка твоих приложений

Docker упрощает цикл разработки, позволяя разработчику работать в стандартизированной среде на локальном контейнере, что поставляет ваши приложения и сервисы. Контейнеры идеальны для работы CI/DI[^2].

[^2]: CI/DI (непрерывная интеграция и непрерывная поставка) - это методология разработки и набор практик, при которых в код вносятся небольшие изменения с частыми коммитами.Подробнее в [статье](https://habr.com/ru/company/otus/blog/515078/)

Рассмотрите следующие примеры ситуаций:
 - Ваши разработчики пишут код локально и делятся им с коллегами с помощью контейнеров.
 - Они используют Docker для поставки приложений в тестовую среду и запуска автоматизированных и ручных тестов.
 - Когда разработчики находят дефекты, они могут исправить их в среде разработки и развернуть еще раз в тестовом контуре для тестирования и проверки.
 - Когда тестирование завершено, отправка патча так же проста, что и развертывание образа на продуктовой среде.
 
### Адаптивная разработка и масштабирование

Платформа на основе контейнеров Docker обеспечивает высокую переносимость нагрузки. Контейнеры могут быть запущены на локальном компьютере разработчика, на физических или виртуальных машинах в дата-центре, облаке или смеси этих сред.

Потративность и легковесность Docker упрощает динамическое управление нагрузкой, расширение или разделение приложений и сервисов в соответствие с нуждами бизнеса в реальном времени.

### Запуск большей нагрузки на сервере

Docker быстр и легковесен. Он предлагает затрато-эффективную альтернативу гипервизорам[^3] виртуальных машин, поэтому вы можете использовать большую вычислительную мощность для достижения своей бизнес-цели. Docker идеально подходит для нагруженных сред, где требуется сделать большее, но с меньшими ресурсами. 

[^3]: Гипервизор или монитоор виртуальных машин — программа или аппаратная схема, обеспечивающая или позволяющая одновременное, параллельное выполнение нескольких операционных систем на одном и том же хост-компьютере.

## Архитектура Docker

Docker использует архтектуру "клиент-сервер". Клиент Docker-а обращается к службе, что управляет поднятием тяжелых сборок, их запуском и размещением контейнеров. Клиент и служба могут быть запущены в одной системе или удаленно. Они взаимодействуют с помощью REST API, через сокеты UNIX или сетевой интерфейс. Еще один вид Docker клиента - Docker Compose, что позволяет вам работать с приложениями, состоящими из набора контейноров.

![Docker Architecture Diagram](https://docs.docker.com/engine/images/architecture.svg)

## Docker daemon

Служба Docker (`dockerd`) перехватывает запросы Docker API requests и управляет объектами: образов, контейнеров, сетей и файловых хранилищ. Также она взаимодействует с другими службами для управления Docker сервисами.

## Docker Client

Клиент Docker (`docker`) это основной способ взаимодействия множества пользователей. Когда вы используете команды, например, `docker run`, клиент отправляет их для выполнения в [`dockerd`](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#%D1%81%D0%BB%D1%83%D0%B6%D0%B1%D0%B0-docker). Команды используют Docker API. Клиент может взаимодействовать с несколькими службами.

## Docker Desktop

Настольный Docker легок для установки на Mac или Windows средах, что позволяет вам собирать и делиться упакованными в контейнер приложениями и сервисами. Натольный Docker включает в себя службу Docker ([`dockerd`](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#%D1%81%D0%BB%D1%83%D0%B6%D0%B1%D0%B0-docker)), Docker клиента ([`docker`](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#docker-client)), Docker Compose, Docker Content Trust, Kubernetes и Credential Helper. Подробная информация в статье [Docker Desktop]().

## Docker registry
Docker registry предназначен для хранения образов. Docker Hub - это открытый реестр для общего пользования, также является дефолтным при поиске образов в Docker. Есть возможность запуска собственного приватного реестра.

Когда вы используете `docker pull` или `docker run`, нужные образы импортируются из настроенного вами реестра. При использовании команды `docker push` ваш образ экспортируется в ваш приватный реестр.

## Объекты Docker
Когда вы работаете с Docker, вы создаете и используете образы, контейнеры, сети, файловые хранилища, плагины и другие объекты. Эта секция посвящена быстрому обзору некоторых объектов. 

### Образы
Образ - это читаемый шаблон с инструкциями для создания Docker контейнера. Часто, он может наследовать от другого образа с некоторыми настраиваемыми добавлениями. Например, вы собираете образ, что был основан на образе `ubuntu`, но также устанавливает Apache web server и ваше приложение вместе с конфигурацией, необходимой для запуска.

Вы можете создавать свои собственные образы или использовать чужие, что были опубликованы в реестре. Для его сборки, вам требуется составить Dockerfile с простым синтаксисом для определения шагов, необходимых для создания образа и его запуска. Каждая инструкция в Dockerfile создает новый слой образа. Когда вы изменяете Dockerfile и пересобираете образ, пересоздаются только отредактированные слои. Вот что делает образы такими легковесными, маленькими и быстрыми в сравнении с другими технологиями виртуализации.

### Контейнеры
Контейнер - это запускаемая единица образа. Вы можете создавать, запускать, останавливать, перпемещать или удалять контейнер с помощью Docker API или CLI. Вы можете соединять контейнер к более. чем одной, сети, прикреплять к нему хранилище или даже создавать новый образ на основе его текущего состояния.

Контейнеры по умолчанию относительно хорошо изолированы от друг друга и хоста, на котором запущены. Вы можете контролировать изолированность сети, хранилища или других прилегающих подсистем от остальных контейнеров и хоста.

Контейнер определяется своим образом и любой конфигурацией, что вы настроили на момент создания или запуска. Когда контейнер удаляют, любые изменения его состояния, что не хранятся в постоянном хранилище, стираются.

### Пример команды `docker run`
Следующая команда запускает `ubuntu` контейнер через `/bin/bash`, интерактивно прикреплясь к вашей локальной сессии командной строки:

 > `$ docker run -i -t ubuntu /bin/bash`
 
 Когда вы запускаете эту команду, происходит следующее (предполагая, что используется конфигурация реестра по умолчанию):

1. Если у вас нет локального образа ubuntu, Docker вытягивает его из сконфигурированного вами реестра, как если бы вы вручную запустили `docker pull ubuntu`.
2. Docker создает новый контейнер, как с помощью команды `docker container create`.
3. Docker назначает контейнеру файловую систему для чтения/записи, как финальный слой. Это позволяет запущенному контейнеру создавать или редактировать файлы и директории своего локального хранилища.
4. Docker создает сетевой интерфейс для соединения контейнера с сетью по умолчанию, т.к. вы не указали специальные сетевые настройки. Это также включает в себя назначение IP адреса. По умолчанию, контейнеры могут обращаться к внешним сетям с помощью сетевого соединения хоста.
5. Docker запускает контейнер и исполняет `/bin/bash`. Т.к. контейнер запускается интерактивно и прикрепляется к вашему терминалу (из-за флагов `-i` и `-t`), вы можете вводить команды с помощью клавиатуры, а вывод будет логгироваться в вагем терминале.
6. Когды вы печатаете `exit` для остановки команды `/bin/bash`, контейнер останавливается, но не удаляется. Вы можете перезапустить или стереть его.

## Лежащие в основе технологии
Docker разработан на языке [Go](https://go.dev/) и использует преимущества некоторых функций ядра Linux для обеспечения его функциональности. Технология, называемая `namespaces`, позволяет создавать изолированные пространства - контейнеры. Когда вы запускаете контейнер, Docker создает для него набор пространств.

Эти пространства создают слой изоляции. Каждый аспект контейнера запущен в отдельном пространстве и имеет к нему ограниченный доступ.
