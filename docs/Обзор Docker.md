# Обзор Docker
Docker это открытая платформа для разработки, поставки и запуска приложений. Докер позволяет вам отделить ваши приложения от инфраструктуры, что ускоряет поставку программ. С Docker вы можете настраивать инфраструктуру таким же образом, что и приложения. Используя преимущества методик Docker для быстрой поставки, тестирования и развертывания кода, вы можете значительно уменьшить задержку между написанием кода и его запуском на производственной среде.
## Платформа Docker
Docker дает возможность упаковать приложение со всеми зависимостями и запустить его в изолированной среде, называемой *контейнером*. Изоляция и защищенность позволяет запускать много контейнеров одновременно на одном хосте. Контейнеры легковесны и содержат все, что необходимо для запуска приложения, так что вам не нужно полагаться на то, что в данный момент уже установлено на хосте. Вы можете легко ~~делиться~~ контейнерами и быть уверенным, что все получают точно такой же контейнер, работающий тем же образом.

Docker предусматривает утилиты и платформу для управления циклом жизни ваших контейнеров:

 - Разработка приложения и поддержка его компонентов с помощью контейнеров.
 - Контейнер становится ~~единицей~~ для распределения и тестирования ваших приложений.
 - Когды все готово, разверните свое приложение в свою производственную среду как контейнер или оркестированный[^1] сервис. Это работает одинаково независимо от того, ваша производтвенная среда это локальный дата-центр, облачный ~~поставщик~~ или их смесь.
 
 [^1]: Оркестированние - автоматическая конфигурация, управление и координация компьютерных систем, приложений и сервисов.

## Для чего можно использовать Docker?
> Быстрая и последовательная поставка твоих приложений

Docker упрощает цикл разработки, позволяя разработчику работать в стандартизированной среде на локальном контейнере, что поставляет ваши приложения и сервисы. Контейнеры идеальны для работы CI/DI[^2].

[^2]: CI/DI (непрерывная интеграция и непрерывная поставка) - это методология разработки и набор практик, при которых в код вносятся небольшие изменения с частыми коммитами.Подробнее в [статье](https://habr.com/ru/company/otus/blog/515078/)

Рассмотрите следующие примеры ситуаций:
 - Ваши разработчики пишут код локально и делятся им с коллегами с помощью Docker контейноров.
 - Они используют Докер для отправки приложений в тестовую среду и ~~исполнения~~ автоматизированных и ручных тестов.
 - Когда разработчики находят дефекты, они могут исправить их в среде разработки и развернуть еще раз в тестовом контуре для тестирования и проверки.
 - Когда тестирование завершено, отправка патча так же проста, что и развертывание образа на продуктовой среде.
 
### Адаптивная разработка и масштабирование

Платформа на основе контейнеров Docker обеспечивает высокую переносимость нагрузки. Контейнеры могут быть запущены на локальном компьютере разработчика, на физических или виртуальных машинах в дата-центре, облаке или ~~смечи~~ этих сред.

Потративность и легковесность Docker упрощает динамическое управление нагрузкой, расширение или ~~разделение~~ приложений и сервисов в соответствие с нуждами бизнеса в реальном времени.

### Запуск большей нагрузки на одном ~~сервере~~

Docker быстр и легковесен. Он предлагает ~~работоспособную~~ и затрато-эффективную альтернативу ~~мониторинговым~~ виртуальным машинам, поэтому вы можете использовать большую вычислительную мощность для достижения своей бизнес-цели. Docker идеально подходит для ~~нагруженных~~ сред и маленьких или средних развертываний, где требуется сделать большее, но с меньшими ресурсами. 

## Архитектура Docker

Docker использует ~~модель~~ клиент-сервер. Клиент Docker-а обращается к службе, что управляет поднятием тяжелых сборок, их запуском и ~~распределением~~ контейнеров. Клиент и служба могут быть запущены в одной системе или удаленно. Они взаимодействуют с помощью REST[^3] API, через сокеты UNIX[^4] или сетевой интерфейс. Еще один вид Docker клиента - Docker Compose, что позволяет вам работать с приложениями, состоящими из набора контейноров.

[^3]: REST API (Representational State Transfer) -  архитектурный стиль взаимодействия компонентов распределённого приложения в сети. Подробнее в [статье](https://habr.com/ru/post/483202/).
[^4]: UNIX - 

![Docker Architecture Diagram](https://docs.docker.com/engine/images/architecture.svg)

## Docker daemon

Служба Docker (dockerd) ~~прослушивает~~ запросы Docker API requests и управляет такими объектами, как: образы, контейнеры, сети и ~~файловые хранилища~~. Также она взаимодействует с другими службами для управления Docker сервисами.

## Docker Client

Клиент Docker (docker) это основной способ взаимодействия множества пользователей. Когда вы используете команды, например, `docker run`, клиент отправляет их для выполнения в [dockerd](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#%D1%81%D0%BB%D1%83%D0%B6%D0%B1%D0%B0-docker). Команды используют Docker API. Клиент может взаимодействовать с несколькими службами.

## Docker Desktop

Настольный Docker легок для установки на Mac или Windows средах, что позволяет вам собирать и делиться упакованными в контейнер приложениями и сервисами. Натольный Docker включает в себя службу Docker ([dockerd](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#%D1%81%D0%BB%D1%83%D0%B6%D0%B1%D0%B0-docker)), Docker клиента ([docker](https://github.com/gfg7/docker-docs-rus/edit/draft/docs/%D0%9E%D0%B1%D0%B7%D0%BE%D1%80%20Docker.md#docker-client)), Docker Compose, Docker Content Trust, Kubernetes и Credential Helper. Подробная информация в статье [Docker Desktop]().

## Docker реестры
Реестр Docker предназначени для хранения образов. Docker Hub - это открытый реестр для общего пользования, также является дефолтным при поиске образов в Docker. Есть возможность запуска собственного приватного реестра.

Когда вы используете `docker pull` или `docker run`, нужные образы импортируются из настроенного вами реестра. При использовании команды `docker push` ваш образ экспортируется в ваш приватны реестр.

## Docker objects
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

### Images
An image is a read-only template with instructions for creating a Docker container. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

### Containers
A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

### Example docker run command
The following command runs an ubuntu container, attaches interactively to your local command-line session, and runs /bin/bash.

 docker run -i -t ubuntu /bin/bash
When you run this command, the following happens (assuming you are using the default registry configuration):

If you do not have the ubuntu image locally, Docker pulls it from your configured registry, as though you had run docker pull ubuntu manually.

Docker creates a new container, as though you had run a docker container create command manually.

Docker allocates a read-write filesystem to the container, as its final layer. This allows a running container to create or modify files and directories in its local filesystem.

Docker creates a network interface to connect the container to the default network, since you did not specify any networking options. This includes assigning an IP address to the container. By default, containers can connect to external networks using the host machine’s network connection.

Docker starts the container and executes /bin/bash. Because the container is running interactively and attached to your terminal (due to the -i and -t flags), you can provide input using your keyboard while the output is logged to your terminal.

When you type exit to terminate the /bin/bash command, the container stops but is not removed. You can start it again or remove it.

## The underlying technology
Docker is written in the Go programming language and takes advantage of several features of the Linux kernel to deliver its functionality. Docker uses a technology called namespaces to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container.

These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

## Next steps
Read about installing Docker.
Get hands-on experience with the Getting started with Docker tutorial.
