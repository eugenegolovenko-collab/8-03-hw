# Домашнее задание к занятию `«GitLab»` - `Евгений Головенко`

---

### Задание 1

**Что нужно сделать:**

1. Разверните GitLab локально, используя Vagrantfile и инструкцию, описанные в [этом репозитории](https://github.com/netology-code/sdvps-materials/tree/main/gitlab).   
2. Создайте новый проект и пустой репозиторий в нём.
3. Зарегистрируйте gitlab-runner для этого проекта и запустите его в режиме Docker. Раннер можно регистрировать и запускать на той же виртуальной машине, на которой запущен GitLab.

В качестве ответа в репозиторий шаблона с решением добавьте скриншоты с настройками раннера в проекте.

---

> Примечание: вариант с Vagrant не был использован из-за проблем с вложенными виртуальными машинами (`VT-x is not available (VERR_VMX_NO_VMX)`). Принято решение поднять GitLab через Docker Compose на хостовой Ubuntu VM, что принципиально не противоречит условиям задания.

1. Запуск GitLab

Создана рабочая директория:

```
mkdir -p ~/gitlab-docker
cd ~/gitlab-docker
```

docker-compose.yml:

```
version: '3.8'

services:
  gitlab:
    image: 'gitlab/gitlab-ce:latest'
    container_name: gitlab
    restart: always
    hostname: 'gitlab.local'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://localhost:8181'
    ports:
      - '8181:80' #порт 8080 нв VM уже занят jenkins
      - '443:443'
      - '2222:22' #порт 22 на хосте уже занят
    volumes:
      - './config:/etc/gitlab'
      - './logs:/var/log/gitlab'
      - './data:/var/opt/gitlab'

gitlab-runner:
    image: gitlab/gitlab-runner:latest
    container_name: gitlab-runner
    restart: always
    volumes:
      - '/var/run/docker.sock:/var/run/docker.sock'
      - './runner-config:/etc/gitlab-runner'
```

Запуск GitLab:

```
docker-compose up -d
```

Проверка логов:

```
docker logs -f gitlab
```

Пароль для первого входа:

```
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```

Далее 

GitLab развернут в Docker, веб-интерфейс доступен по адресу:  
[http://localhost:8181](http://localhost:8181)

2. Создание проекта
   
В GitLab веб-интерфейсе:

`Create new project -> Blank project`

Создан пустой проект в GitLab: `homework-8-03`

3. Регистрация GitLab Runner

Использую контейнер Runner:

```
sudo docker exec -it gitlab-runner gitlab-runner register
```

GitLab Runner зарегистрирован с параметрами:

- **GitLab instance URL:** `http://172.17.0.1:8181`  
- **Registration token:** (GR1234567890tp1sN-SU8BuGaGaW)  
- **Description:** `docker-runner`  
- **Tags:** `docker,ci`  
- **Maintenance note:** `Homework 8-03`  
- **Executor:** `docker`  
- **Default Docker image:** `golang:1.17`  

> Для подключения Runner к GitLab используется IP Docker-хоста, иначе Runner не видит GitLab.

Runner появился в GitLab -> Project -> CI/CD Settings -> Runners 

## Скриншоты с настройками раннера

<img width="1016" height="868" alt="Capture_runner" src="https://github.com/user-attachments/assets/0c15938b-2158-46bb-9db6-27b3ccef2513" />

<img width="1018" height="711" alt="Capture_runner_2" src="https://github.com/user-attachments/assets/27091b7c-5e3d-4c45-8f4e-b961f1a7d14c" />

---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
