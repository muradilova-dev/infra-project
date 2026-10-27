# Infra project

Учебный инфраструктурный репозиторий курса 

<!-- Допишите сюда -->
Training project: Docker and Ansible web server setup.
Это изменение сделано через веб-интерфейс GitHub. Всем привет
## Запуск в Docker

```console
docker build -t infra-web:1.0 docker
docker run -d --name infra-web -p 8080:80 infra-web:1.0
curl http://localhost:8080

Test.
