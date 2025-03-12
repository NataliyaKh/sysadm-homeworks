# Домашнее задание к занятию «Инструменты Git». Наталия Ханова. 

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Инструкция к заданию

1. Склонируйте [репозиторий](https://github.com/hashicorp/terraform) с исходным кодом Terraform.
2. Создайте файл для ответов на задания в своём репозитории, после выполнения прикрепите ссылку на .md-файл с ответами в личном кабинете.
3. Любые вопросы по решению задач задавайте в чате учебной группы.

------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.

**git show aefea**

![Хеш](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_show_aefea.png)

Полный хеш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Комментарий: Update CHANGELOG.md

2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?

**git show 85024d3**

![Тег](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_show_85024d3.png)

Тег: v0.12.23


* Сколько родителей у коммита `b8d720`? Напишите их хеши.

Чтобы познакомиться с родителями коммита, используем команду **git show b8d720^**

![Родители](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_show_parents.png)

Мы видим, что у коммита два родителя, и используем обычную команду **git show**, чтобы увидеть полные хеши каждого из них. 

![Родитель1](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_show_parent1.png)

![Родитель2](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_show_parent2.png)

Хеш родителя 1: 58dcac4b798f0a2421170d84e507a42838101648

Хеш родителя 2: ffbcf55817cb96f6d5ffe1a34abe963b159bf34e

* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.

Можно использовать команду **git log v0.12.23..v0.12.24 --oneline**, но чтобы видеть полные хеши, необходимо прибегнуть к ключу **--format**: **git log v0.12.23..v0.12.24 --format="%H %s"**

![Интервал](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_log_between.png)

* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).

Ищем коммиты с упоминанием функции `func providerSource`:

**git log -S 'func providerSource' --oneline**

![Функция](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_log_function_commit.png)

Сравниваем упоминания функции в двух найденных коммитах:
**git show 8c928e8358 | grep "func providerSource"**
**git show 5af1e6234a | grep "func providerSource"**

![Сравнение](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_log_function_commit_compare.png)

При помощи команды **git log -S 'func providerSource'** можем сравнить и время двух коммитов. 

![8c928e8358](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_log_function_commit1.png)

![5af1e6234a](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_log_function_commit2.png)

Таким образом, функция была создана в более раннем коммите 8c928e8358 (полный хеш 8c928e83589d90a031f811fae52a81be7153e82f). 

* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.

При помощи команды **git log -S 'globalPluginDirs' --oneline --reverse** находим все коммиты с упоминанием функции. 

![globalPluginDirs](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_globalPluginDirs.png)

В первом из них функция была создана, в остальных - отредактирована. Таким образом, в список включим все коммиты, кроме хронологически первого: 

```
c0b1761096 prevent log output during init
35a058fb3d main: configure credentials from the CLI config file
7c7e5d8f0a Don't show data while input if sensitive
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
125eb51dc4 Remove accidentally-committed binary
65c4ba7363 Remove terraform binary
7c4aeac5f3 stacks: load credentials from config file on startup (#35952)
```

Исправление: более корректен поиск по **git log -L :GlobalPluginDirs:plugins.go**. 
В каждом из коммитов, отображённых по команде, описана история изменений функции. В части коммитов изменяется её название - с globalPluginDirs на GlobalPluginDirs, поэтому поиск по **git log -L :globalPluginDirs:plugins.go** не выдаёт актуальных результатов. 

* Кто автор функции `synchronizedWriters`? 

**git log -S 'synchronizedWriters' --reverse**

![author](https://github.com/NataliyaKh/sysadm-homeworks/blob/main/02-git-04-tools/git_commit_author.png)

Автор функции (в его коммите она появилась впервые) - Martin Atkins <mart@degeneration.co.uk>.

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

---

### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.

### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.
