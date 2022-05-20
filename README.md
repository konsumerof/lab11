## Отчёт
1. Установил необходимые утилиты: ngrok, tmux, libevent, ncurses
```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz # скачиваем архим libevent
$ tar -xvzf libevent-2.1.8-stable.tar.gz # разархивируем его
$ cd libevent-2.1.8-stable # перемещаемся в папку с ним
$ ./configure --prefix=${HOME_PREFIX} # указываем путь до директории для установки
$ make && make install # устанавливаем
$ cd .. # перемещаемся в родительскую папку

$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz # скачиваем архив ncurses
$ tar -xvzf ncurses.tar.gz # разархивируем его
$ cd ncurses-5.9 # перемещаемся в папку созданную после распаковывания
$ ./configure --prefix=${HOME_PREFIX} # указываем путь до установки
$ make && make install # устанавливаем
$ cd .. # перемещаемся в родительский каталог

$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz # скачиваем архив tmux
$ tar -xvzf tmux-2.5.tar.gz # разархивируем его
$ cd tmux-2.5 # перемещаемся в папку созданную после распаковывания
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install # устанавливаем
$ cd ..

$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip # скачиваем архив ngrok
$ unizp ngrok-stable-linux-amd64.zip # распаковываем его
$ mv ngrok ${HOME_PREFIX}/bin # перемещаем ngrok в другую директорию
```
2. Авторизировался на https://ngrok.com с помощью GitHub, чтобы получить токен для авторизации туннеля в ngrok
3. С помощью команды tmux new -s session создал новую сессию для ngrok
4. Подключил ngrok к терминалу
```sh
$ export NGROK_TOKEN=<токен> # создаем переменную окружения
$ ngrok authtoken ${NGROK_TOKEN} # авторизуемся в ngrok
$ ngrok tcp 22 # указываем тип протокола и порт подключения
```
![Снимок экрана от 2022-05-20 22-55-38](https://user-images.githubusercontent.com/90759633/169601997-cd5d3b77-4778-41a5-b73d-4e0337083476.png)

![Снимок экрана от 2022-05-20 22-55-32](https://user-images.githubusercontent.com/90759633/169601975-1285ad77-9aac-41e7-a19f-a8610b946b49.png)

5. Теперь с помощью SSH или tmux можно подключиться к локальному сеансу для совместной разработки с помощью порта (в нашем случае 22 порт по протоколу tcp)
```sh
tmux a -t session
ssh ${USERNAME}@0.tcp.ngrok.io -p 22
```

## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

```sh
$ open https://ngrok.com/
```

## Tasks

- [x] 1. Ознакомиться со ссылками учебного материала
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ cd ~ # переходим в корень
$ mkdir install # создаем папки install и tmp
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install # создаем переменные окружения
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```

```sh
$ cd tmp # переходим в папку tmp
```

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz # скачиваем архим libevent
$ tar -xvzf libevent-2.1.8-stable.tar.gz # разархивируем его
$ cd libevent-2.1.8-stable # перемещаемся в папку с ним
$ ./configure --prefix=${HOME_PREFIX} # указываем путь до директории для установки
$ make && make install # устанавливаем
$ cd .. # перемещаемся в родительскую папку
```

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz # скачиваем архив ncurses
$ tar -xvzf ncurses.tar.gz # разархивируем его
$ cd ncurses-5.9 # перемещаемся в папку созданную после распаковывания
$ ./configure --prefix=${HOME_PREFIX} # указываем путь до установки
$ make && make install # устанавливаем
$ cd .. # перемещаемся в родительский каталог
```


```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz # скачиваем архив tmux
$ tar -xvzf tmux-2.5.tar.gz # разархивируем его
$ cd tmux-2.5 # перемещаемся в папку созданную после распаковывания
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install # устанавливаем
$ cd ..
```

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip # скачиваем архив ngrok
$ unizp ngrok-stable-linux-amd64.zip # распаковываем его
$ mv ngrok ${HOME_PREFIX}/bin # перемещаем ngrok в другую директорию
```

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib # создаем переменные окружения
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux # запускаем tmux
```

```sh
$ cd ~
$ rm -rf tmp install # уадляем папки tmp и install
```

```sh
$ brew install tmux ngrok # or use linuxbrew 🎉
```

```sh
$ tmux new -s session_with_group # запускаем новую сессию в tmux
```

```sh
# Alisa:
$ open https://ngrok.com/signup # переходим на сайт для регистрации
$ export NGROK_TOKEN=<токен> # создаем переменную окружения
$ ngrok authtoken ${NGROK_TOKEN} # авторизуемся в ngrok
$ ngrok tcp 22 # указываем тип протокола и порт подключения
<порт_ngrok_сервера>
```

```sh
# Bob:# для работы необходимо предварительно запустить виртуальную машину из прошлой ЛР
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера>
<пароль_от_учетной_записи>
$ tmux a -t session_with_group # подключаемся к созданной сессии
$ <C-B>"
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
Copyright (c) 2015-2021 The ISC Authors
```
