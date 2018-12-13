Чтобы скопировать файл в контейнер необходимо, чтобы файл находился в рабочей директории или в её поддиректориях. В **dockerfile** при этом нужно прописать следующую команду:
```dockerfile
COPY <RELATIVE TO WORK DIRECTORY PATH NAME> <ABSOLUTE PATH NAME IN CONTAINER>
```
Например, у вас есть **dockerfile** с именем **awesome.dockerfile**, находящийся в директории */home/user/repo/docker-files* и файл с именем **test.md**, расположенный в папке */home/user/repo/files*. Его необходимо скопировать в контейнер в папку */opt/myfiles*. Тогда **dockerfile** может быть таким:
```dockerfile
FROM debian:6.0.8
COPY test.md /opt/myfiles/test.md
```
Сборка контейнера тогда может быть такой:
```bash
cd /home/user/repo/files
docker build -f ../docker-files/awesome.dockerfile -t <CONTAINER NAME> .
```
