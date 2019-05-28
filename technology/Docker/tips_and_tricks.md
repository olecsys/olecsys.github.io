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

Для того, чтобы запустить `Docker` в `Windows` как сервис необходимо зарегистрировать `dockerd.exe` в качестве сервиса(выполнять с правами `Администратора`):
```bat
cd C:\Program Files\Docker\Docker\resources
dockerd.exe --register-service
```
После выполнения команды в списке служб появится служба `Docker Engine`. Не путайте с `Docker Desktop Service`. Службу `Docker Desktop Service` можете смело отключать. Также для корректной работы измените `Тип запуска` службы `Docker Engine` на `Автоматически(отложенный запуск)`.
Далее в папке `C:\PrgramData\docker\config` создайте файл `daemon.json` и добавьте туда свою конфигурацию. Обязательно добавьте туда настройку `group` с пользовательской группой, которую создал установщик `Docker` и выставите настройку `experimental` в `true`. В моей версии это пользовательская группа `docker-users`. Минимальная настройка `daemon.json` будет выглядеть следующим образом:
```json
{
    "group": "docker-users",
    "experimental": true
}
```
Далее добавьте всех пользователей `Windows`, которые будут использовать `Docker`, в вашу пользовательскую группу(`docker-users` или что-то еще). Можете сделать это с помощью `Windows` утилиты `lusrmgr.msc`. Для работы `Linux` контейнеров под `Windows` в режиме `LCOW` вам необходимо в папке `Program Files` создать папку `Linux Containers`, скачать [отсюда](https://github.com/linuxkit/lcow/releases) один из `release.zip` и распаковать его в папку `Program Files\Linux Containers`.

Для обновления `Docker` под `Windows` необходимо открыть `Powershell` и ввести:
```powershell
Install-Package -Name docker -ProviderName DockerMsftProvider -Force
```

https://stefanscherer.github.io/sneak-peek-at-lcow/


Для использования образов `balenalib/rpi-raspbian`, эмулирующих `Raspberry Pi`, необходимо, чтобы был установлен пакет `qemu` и `qemu-user-static`. На `Ubuntu` установка выполняется следующим образом:
```bash
sudo apt-get install qemu qemu-user-static
```