# MAC OS

---

## Установка дополнительной программы для работы с командной строкой и настройка конфигурации GIT.

1. Установите менеджер пакетов Homebrew.

Перейдите на официальный сайт Homebrew.
Скопируйте команду для установки — справа от неё есть символ для копирования.
Нажмите на него, чтобы команда попала в буфер обмена.

2. После установки выполните в терминале команду
```$ brew install git```
3. Проверьте установку командой
```$ git version```
если выводится версия git, все успешно.

4. Настройте файл конфигурации для совместной работы .gitconfig:
$ git config --global user.name "ваше имя или ник латиницей" 
$ git config --global user.email ваша электронная почта

5. Убедитесь, что данные сохранились, с помощью одной из двух команд.
```$ cat ~/.gitconfig```
```$ git config --list```

## Работа с локальным репозиторием.

1. Создаем папку в которой мы будем размещать проект, все помнят, что это
```$ mkdir "имя папки"```
и созадем репозиторий командой
```$ git init```

2. Проверяем, что репозиторий создан:
``` $ git status```

3. Если мы ошиблись с папкой, то ее можно разгитить:
```$ cd <папка с репозиторием>```
```$ rm -rf .git``` 

Добавляем файлы в репозиторий и коммитем их.

1. Подготовить файлы к сохранению:
 
```$ git add --all #добавляем все файлы```
или
```$ git add "имя файла"```
и проверяем статус (команда указана выше)

2. Выполнение коммита осуществляется командой:
```$ git commit -m "Название коммита"```

3. Просмотреть историю коммитов можно командой:
```$ git log```

## Работа с удаленным репозиторием GIT HUB

1. Прежде чем начать работать необходимо зарегистрироваться.

2. Зайдите в свой профиль по ссылке https://github.com/username, 
где username — имя, которое вы указали при регистрации.

3. Создайте новый проект, нажав на кнопку New и следуйте инструкции, тут все 
понятийно.

4. Теперь нам необходимо подключится к удаленому репозиторию, 
сделем это через SSH:
Обычно SSH-ключи находятся в директории .ssh/, если папка пуста, 
то ключи необходимо сгенерировать(как это сделать спросите у Поисковика, он 
подскажет).После генерации ключа, копируем содержание публичного ключа и 
добавляем его в пункт меню настроек SSH and GPG keys.

5. Проверьте правильность подключения командой:
```$ ssh -T git@github.com```

6. Теперь нам необходимо связать удаленый и локальный репозиторий, 
делается это с помощью команды:
```$ git remote add origin git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ ПРОЕКТА%```
, например:
```$ git remote add origin git@github.com:dan/project1```

7. Проверить, что это успешно делаем с помощью команды:
```$ git remote -v```
,после ее выполнения появится сообщение
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
Локальный и удаленный репозитории связаны. 

## Синхроизация репозиториев.

1. Самая первая ветка в репозитории появляется автоматически и называется main
(англ. «основная») или master. Её имя нужно указывать при отправке коммитов на
удалённый репозиторий или при получении их из него.

2. Первый раз это надо сделать с помощью команды:
```$ git push -u origin main(или master)```

если увидите сообщение, показанное ниже, то все произошло удачно:

```
remote: Resolving deltas: 100% (1/1), done.
To github.com:danism51/d1
 * [new branch]      master -> master
branch 'master' set up to track 'origin/master'

 ```

3. Последующие сообщения можно делать просто, используя команду:
```$ git push```

## Хеш — идентификатор коммита.

Хеширование (от англ. hash, «рубить», «крошить», «мешанина») — это способ преобразовать набор данных и получить их «отпечаток» (англ. fingerprint).
Git хеширует (преобразует) информацию о коммите с помощью алгоритма SHA-1 (от англ. Secure Hash Algorithm — «безопасный алгоритм хеширования»)
и получает для каждого коммита свой уникальный хеш — результат хеширования.

Хеш — основной идентификатор коммита
Git хранит таблицу соответствий хеш → информация о коммите. Если вы знаете хеш, вы можете узнать всё остальное:
автора и дату коммита и содержимое закоммиченных файлов. Можно сказать, что хеш — основной идентификатор коммита.

Все хеши и таблицу хеш → информация о коммите Git сохраняет в служебные файлы. Они находятся в скрытой папке ```.git``` в репозитории проекта.

## Исследуем лог.

После вызова ```git log``` появляется список коммитов.

Разберём элементы, из которых состоит описание:

- строка из цифр и латинских букв после слова commit — это хеш коммита;
- Author — имя автора и его электронная почта;
- Date — дата и время создания коммита;
- в конце находится сообщение коммита, т.е. то, как вы описали свой коммит.

Если в репозитории много коммитов — например, сотни или тысячи,  то можно быстро найти нужный по описанию используя сокращенный лог.
```git log --oneline```

## HEAD — всему голова.

При вызове команды ```git log``` вы могли заметить надпись (HEAD -> master) после хеша одного из коммитов.
Файл ```HEAD``` (англ. «голова», «головной») — один из служебных файлов папки ```.git```. Он указывает на коммит, который сделан последним (то есть на самый новый).

Внутри ```HEAD``` — ссылка на служебный файл: ```refs/heads/master``` (или ```refs/heads/main``` в зависимости от названия ветки). 
Если заглянуть в этот файл, можно увидеть хеш последнего коммита. 

## Статусы файлов в Git.

Одна из ключевых задач Git — отслеживать изменения файлов в репозитории. Для этого каждый файл помечается каким-либо статусом. Рассмотрим основные.

1. ```untracked``` (англ. «неотслеживаемый»)
Мы говорили, что новые файлы в Git-репозитории помечаются как ```untracked```, то есть неотслеживаемые.
Git «видит», что такой файл существует, но не следит за изменениями в нём. У ```untracked```-файла нет предыдущих версий, зафиксированных в коммитах или через команду ```git add```.

2. ```staged``` (англ. «подготовленный»)
После выполнения команды ```git add``` файл попадает в ```staging area``` (от англ. stage — «сцена», «этап [процесса]» и area — «область»), то есть в список файлов, которые войдут в коммит.
В этот момент файл находится в состоянии ```staged```.

3. ```tracked``` (англ. «отслеживаемый»)
Состояние ```tracked``` — это противоположность ```untracked```. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью ```git commit```,
а также файлы, которые были добавлены в staging area командой ```git add```. То есть все файлы, в которых Git так или иначе отслеживает изменения.

4. ```modified``` (англ. «изменённый»)
Состояние ```modified``` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.

Статусы файлов проверяют с помощью команды ```git status```.

В итоге ```git status``` показывает только следующие состояния файлов:
-```staged``` (Changes to be committed в выводе git status);
-```modified``` (Changes not staged for commit);
-```untracked``` (Untracked files).

