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

[^2]: CI/DI (непрерывная интеграция и непрерывная поставка) - это методология разработки и набор практик, при которых в код вносятся небольшие изменения с частыми коммитами. [Подробнее в статье](https://habr.com/ru/company/otus/blog/515078/)

Рассмотрите следующие примеры ситуаций:
 - Ваши разработчики пишут код локально и делятся им с коллегами с помощью Docker контейноров.
 - Они используют Докер для отправки приложений в тестовую среду и ~~исполнения~~ автоматизированных и ручных тестов.
 - Когда разработчики находят дефекты, они могут исправить их в среде разработки и развернуть еще раз в тестовом контуре для тестирования и проверки.
 - Когда тестирование завершено, отправка патча так же проста, что и развертывание образа на продуктовой среде.
 
### Адаптивная разрабтка и масштабирование

Docker’s container-based platform allows for highly portable workloads. Docker containers can run on a developer’s local laptop, on physical or virtual machines in a data center, on cloud providers, or in a mixture of environments.

Docker’s portability and lightweight nature also make it easy to dynamically manage workloads, scaling up or tearing down applications and services as business needs dictate, in near real time.

Running more workloads on the same hardware

Docker is lightweight and fast. It provides a viable, cost-effective alternative to hypervisor-based virtual machines, so you can use more of your compute capacity to achieve your business goals. Docker is perfect for high density environments and for small and medium deployments where you need to do more with fewer resources.

### Running more workloads on the same hardware

Docker is lightweight and fast. It provides a viable, cost-effective alternative to hypervisor-based virtual machines, so you can use more of your compute capacity to achieve your business goals. Docker is perfect for high density environments and for small and medium deployments where you need to do more with fewer resources.

## Docker architecture
Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface. Another Docker client is Docker Compose, that lets you work with applications consisting of a set of containers.
![Docker Architecture Diagram](https://docs.docker.com/engine/images/architecture.svg)

## The Docker daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

## The Docker client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

## Docker Desktop
Docker Desktop is an easy-to-install application for your Mac or Windows environment that enables you to build and share containerized applications and microservices. Docker Desktop includes the Docker daemon (dockerd), the Docker client (docker), Docker Compose, Docker Content Trust, Kubernetes, and Credential Helper. For more information, see Docker Desktop.

## Docker registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry.

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.

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
