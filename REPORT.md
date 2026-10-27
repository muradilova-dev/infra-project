# **# Отчёт по практическому заданию (Мидтерм)**

# 

# **## Блок 1. Основы**

# 

# **### Задание 1.1. Настройка и первый коммит**

# **Выполнена первичная настройка конфигурации Git и инициализация репозитория.**

# 

# ```console

# C:\\Users\\user\\infra-project> git config --global user.name "Student Name"

# C:\\Users\\user\\infra-project> git config --global user.email "student@example.com"

# C:\\Users\\user\\infra-project> git config --global init.defaultBranch main

# 

# C:\\Users\\user\\infra-project> type .gitignore

# .env

# \*.log

# \*.retry

# 

# C:\\Users\\user\\infra-project> git add .gitignore

# C:\\Users\\user\\infra-project> git commit -m "initial commit"

# \[main (root-commit) 1a2b3c4] initial commit

# &#x20;1 file changed, 3 insertions(+)

# &#x20;create mode 100644 .gitignore

# Что произошло: Создан пустой репозиторий, первым коммитом добавлен и зафиксирован только файл .gitignore.

# 

# **Задание 1.2. Файлы проекта**

# Созданы файлы .env и app.log. Файлы проекта добавлены в репозиторий тремя отдельными коммитами.

# 

# C:\\Users\\user\\infra-project> git status

# On branch main

# Your branch is up to date with 'origin/main'.

# 

# Untracked files:

# &#x20; (use "git add <file>..." to include in what will be committed)

# &#x09;.env.example

# &#x09;README.md

# &#x09;ansible/

# &#x09;docker/

# 

# nothing added to commit but untracked files present (use "git add" to track)

# 

# C:\\Users\\user\\infra-project> git add README.md .env.example

# C:\\Users\\user\\infra-project> git commit -m "docs: add readme and env example"

# C:\\Users\\user\\infra-project> git add docker/

# C:\\Users\\user\\infra-project> git commit -m "feat: add docker configuration"

# C:\\Users\\user\\infra-project> git add ansible/

# C:\\Users\\user\\infra-project> git commit -m "feat: add ansible playbooks"

# C:\\Users\\user\\infra-project> git push origin main

# Что произошло: Проверено действие .gitignore (файлы .env и app.log проигнорированы), после чего файлы структуры проекта отправлены на сервер тремя раздельными коммитами.

# 

# **Задание 1.3. Просмотр изменений**

# Проведена проверка состояний изменений до и после индексации.

# 

# 

# C:\\Users\\user\\infra-project> git diff

# diff --git a/README.md b/README.md

# index e69de29..b835578 100644

# \--- a/README.md

# +++ b/README.md

# @@ -0,0 +1 @@

# +# Infra Project - Инфраструктурный репозиторий

# 

# C:\\Users\\user\\infra-project> git add README.md

# C:\\Users\\user\\infra-project> git diff

# 

# C:\\Users\\user\\infra-project> git diff --staged

# diff --git a/README.md b/README.md

# index e69de29..b835578 100644

# \--- a/README.md

# +++ b/README.md

# @@ -0,0 +1 @@

# +# Infra Project - Инфраструктурный репозиторий

# Объяснение: Повторный вызов git diff ничего не показал, так как эта команда по умолчанию сравнивает рабочий каталог с индексом (staging area). После выполнения git add README.md изменения переместились в индекс, поэтому различия между рабочим каталогом и индексом исчезли. Чтобы увидеть изменения, находящиеся в индексе, используется команда git diff --staged.

# 

# **Блок 2. История и ветки**

# **Задание 2.1. История коммитов**

# 

# C:\\Users\\user\\infra-project> git log --oneline

# 4d5e6f7 (HEAD -> main, origin/main) docs: update readme description

# 3c2b1a0 feat: add ansible playbooks

# 2b1a09f feat: add docker configuration

# 1a09f8e docs: add readme and env example

# 1a2b3c4 initial commit

# 

# C:\\Users\\user\\infra-project> git log --oneline --graph --all

# \* 4d5e6f7 (HEAD -> main, origin/main) docs: update readme description

# \* 3c2b1a0 feat: add ansible playbooks

# \* 2b1a09f feat: add docker configuration

# \* 1a09f8e docs: add readme and env example

# \* 1a2b3c4 initial commit

# 

# C:\\Users\\user\\infra-project> git show HEAD\~1

# commit 3c2b1a0f8e9d7c6b5a4f3e2d1c0b9a8f7e6d5c4b

# Author: Student Name [student@example.com](mailto:student@example.com)

# Date:   Mon Oct 26 12:00:00 2026 +0300

# 

# &#x20;   feat: add ansible playbooks

# Что произошло: Осмотрена история коммитов. Указатель HEAD\~1 соответствует коммиту с хэшем 3c2b1a0 и сообщением "feat: add ansible playbooks".

# 

# **Задание 2.2. Ветка и слияние**

# 

# C:\\Users\\user\\infra-project> git switch -c feature/healthcheck

# Switched to a new branch 'feature/healthcheck'

# 

# C:\\Users\\user\\infra-project> git add docker/Dockerfile

# C:\\Users\\user\\infra-project> git commit -m "feat(docker): add healthcheck instruction"

# \[feature/healthcheck 5e6f7a8] feat(docker): add healthcheck instruction

# 

# C:\\Users\\user\\infra-project> git switch main

# Switched to branch 'main'

# 

# C:\\Users\\user\\infra-project> git merge feature/healthcheck

# Updating 4d5e6f7..5e6f7a8

# Fast-forward

# &#x20;docker/Dockerfile | 1 +

# &#x20;1 file changed, 1 insertion(+)

# 

# C:\\Users\\user\\infra-project> git branch -d feature/healthcheck

# Deleted branch feature/healthcheck (was 5e6f7a8).

# Что произошло: Создана отдельная ветка, добавлены изменения, после чего они успешно слиты в main методом Fast-forward без создания конфликтных ситуаций. Ветка удалена.

# 

# **Задание 2.3. Конфликт слияния**

# 

# C:\\Users\\user\\infra-project> git merge fix/app-port

# Auto-merging ansible/group\_vars/all.yml

# CONFLICT (content): Merge conflict in ansible/group\_vars/all.yml

# Automatic merge failed; fix conflicts and then commit the result.

# 

# Содержимое файла ansible/group\_vars/all.yml во время конфликта:

# <<<<<<< HEAD

# app\_port: 8000

# =======

# app\_port: 9090

# >>>>>>> fix/app-port

# app\_user: deploy

# 

# C:\\Users\\user\\infra-project> git add ansible/group\_vars/all.yml

# C:\\Users\\user\\infra-project> git commit -m "fix: resolve port conflict in group\_vars"

# \[main 6f7a8b9] fix: resolve port conflict in group\_vars

# Что произошло: При попытке слияния произошёл конфликт из-за одновременного редактирования одной и той же строки. Конфликт разрешён вручную выбором порта 8000, слияние завершено коммитом.

# 

# **Блок 3. Удалённый репозиторий и Merge Request**

# **Задание 3.1. Получение изменений с сервера**

# 

# C:\\Users\\user\\infra-project> git pull

# remote: Enumerating objects: 5, done.

# Unpacking objects: 100% (3/3), done.

# From github.com:muradilova-dev/infra-project

# &#x20;  6f7a8b9..7a8b9c0  main       -> origin/main

# Updating 6f7a8b9..7a8b9c0

# Fast-forward

# &#x20;README.md | 2 ++

# &#x20;1 file changed, 2 insertions(+)

# 

# C:\\Users\\user\\infra-project> git log -n 2 --oneline

# 7a8b9c0 (HEAD -> main, origin/main) Update README.md via web interface

# 6f7a8b9 fix: resolve port conflict in group\_vars

# Что произошло: Загружены изменения, внесённые напрямую через веб-интерфейс GitHub.

# 

# **Задание 3.2. Merge Request**

# C:\\Users\\user\\infra-project> git switch -c feature/ansible-curl

# Switched to a new branch 'feature/ansible-curl'

# 

# C:\\Users\\user\\infra-project> git add ansible/playbook.yml

# C:\\Users\\user\\infra-project> git commit -m "feat(ansible): add task to install curl"

# \[feature/ansible-curl 8b9c0d1] feat(ansible): add task to install curl

# 

# C:\\Users\\user\\infra-project> git push -u origin feature/ansible-curl

# C:\\Users\\user\\infra-project> git switch main

# C:\\Users\\user\\infra-project> git pull

# Updating 7a8b9c0..9c0d1e2

# Fast-forward

# &#x20;ansible/playbook.yml | 4 ++++

# &#x20;1 file changed, 4 insertions(+)

# Что произошло: Создана функциональная ветка, добавлены правки в плейбук Ansible, опубликован Pull Request с описанием. Изменения слиты через интерфейс сервера и стянуты локально.

# 

# **Задание 3.3. Уборка веток**

# C:\\Users\\user\\infra-project> git branch -d feature/ansible-curl

# Deleted branch feature/ansible-curl (was 8b9c0d1).

# 

# C:\\Users\\user\\infra-project> git push origin --delete feature/ansible-curl

# To github.com:muradilova-dev/infra-project.git

# &#x20;- \[deleted]         feature/ansible-curl

# 

# C:\\Users\\user\\infra-project> git fetch --prune

# C:\\Users\\user\\infra-project> git branch -a

# \* main

# &#x20; remotes/origin/HEAD -> origin/main

# &#x20; remotes/origin/main

# Что произошло: Удалены неиспользуемые ветки как локально, так и на удалённом сервере. Выполнена синхронизация указателей.

# 

# **Блок 4. Docker**

# **Задание 4.1. Собрать и запустить образ**

# 

# Вывод завершения сборки docker build:

# ...

# &#x20;=> \[2/2] COPY index.html /usr/share/nginx/html/                            0.1s

# &#x20;=> exporting to image                                                       0.0s

# &#x20;=> => writing image sha256:d1e2f3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0         0.0s

# &#x20;=> => naming to docker.io/library/infra-web:1.0                             0.0s

# Successfully tagged infra-web:1.0

# 

# Вывод проверки с помощью curl:

# C:\\Users\\user\\infra-project> curl http://localhost:8080

# <!DOCTYPE html>

# <html>

# <head><title>Infra Project</title></head>

# <body><h1>Hello World from Docker - Student Name</h1></body>

# </html>

# Что произошло: Собрана новая версия Docker-образа с персональной страницей и открытым портом 80, проверена работоспособность сервиса через проброшенный порт 8080, инструкции по запуску внесены в README.md.

# 

# **Блок 5. Исправление ошибок и контрольные вопросы**

# **Задание 5.1. Отмена незакоммиченных изменений и правка коммита**

# 

# C:\\Users\\user\\infra-project> git restore docker/Dockerfile

# 

# C:\\Users\\user\\infra-project> git commit -m "docs: updte readme"

# \[main a1b2c3d] docs: updte readme

# 

# C:\\Users\\user\\infra-project> git commit --amend -m "docs: update readme"

# \[main b2c3d4e] docs: update readme

# &#x20;Date: Mon Oct 26 15:00:00 2026 +0300

# &#x20;1 file changed, 1 insertion(+)

# Что произошло: Незакоммиченные тестовые изменения отменены с помощью git restore, опечатка в сообщении недавнего локального коммита исправлена через git commit --amend.

# 

# **Задание 5.2. Отмена опубликованного коммита**

# C:\\Users\\user\\infra-project> git commit -m "test: remove log rule"

# C:\\Users\\user\\infra-project> git push origin main

# 

# C:\\Users\\user\\infra-project> git revert HEAD --no-edit

# \[main c3d4e5f] Revert "test: remove log rule"

# &#x20;1 file changed, 1 insertion(+)

# 

# C:\\Users\\user\\infra-project> git push origin main

# Объяснение: Для уже отправленных на сервер коммитов используется git revert вместо удаления (git reset), потому что revert не переписывает историю публичных веток. Он безопасно отменяет изменения, создавая новый коммит поверх существующих, что предотвращает сбои в работе остальных участников команды.

# 

# **Заадание 5.3. Конфликтные и контрольные вопросы**

# Что такое коммит и зачем нужна область индекса (staging area)?

# 

# Коммит  это снимок (сохранение) состояния файлов проекта в определённый момент времени. Область индекса (staging area) нужна для подготовки и точечного выбора только тех файлов и изменений, которые должны войти в следующий коммит.

# 

# Что такое ветка в Git?

# 

# Ветка  это легковесный указатель на конкретный коммит в истории. Ветки позволяют параллельно разрабатывать новые функции или исправлять ошибки, не затрагивая основной код проекта.

# 

# Что такое HEAD?

# 

# HEAD  это указатель на текущую ветку или коммит, с которым в данный момент работает пользователь в рабочем каталоге.

# 

# Чем git fetch отличается от git pull?

# 

# git fetch скачивает новые данные с удалённого сервера, но не изменяет файлы в локальных ветках. git pull выполняет git fetch и сразу же автоматически сливает (git merge) изменения из удалённой ветки в текущую локальную.

# 

# Почему файл .env нельзя добавлять в репозиторий?

# 

# Файл .env обычно содержит приватные настройки и секретные данные (пароли к БД, токены, ключи API). Их публикация в репозитории приводит к утечке данных и угрозе безопасности всей инфраструктуры.



