# Домашнее задание к занятию «Инструменты Git»

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

1. >Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
git log показывает все хеши, в которых есть указанное совпадение, в первую очередь при этом идет совпадение с начала хеша. Дальнейшее выполнение прерываем нажатием q:
```
git log aefea
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400

    Update CHANGELOG.md

````

2. Ответьте на вопросы.

* >Какому тегу соответствует коммит `85024d3`?
Аналогично предыдущему. Тег будет написан рядом с хешом коммита в скобках.

```
git log 85024d3
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000

    v0.12.23
```

 * >Сколько родителей у коммита `b8d720`? Напишите их хеши.
Это merge-коммит, поэтому родителей у него два. Их хеши:
```
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git show b8d720^
commit 56cd7859e05c36c06b56d013b55a252d0bb7e158
Merge: 58dcac4b79 ffbcf55817

seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git show 58dcac4b79 | head -n 1
commit 58dcac4b798f0a2421170d84e507a42838101648
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git show ffbcf55817 | head -n 1
commit ffbcf55817cb96f6d5ffe1a34abe963b159bf34e
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ 
```

 * >Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.

```
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git log 'v0.12.23..v0.12.24' --oneline
33ff1c03bb (tag: v0.12.24) v0.12.24
b14b74c493 [Website] vmc provider links
3f235065b9 Update CHANGELOG.md
6ae64e247b registry: Fix panic when server is unreachable
5c619ca1ba website: Remove links to the getting started guide's old location
06275647e2 Update CHANGELOG.md
d5f9411f51 command: Fix bug when using terraform login on Windows
4b6d06cc5d Update CHANGELOG.md
dd01a35078 Update CHANGELOG.md
225466bc3e Cleanup after v0.12.23 release
```

 * >Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
Раз нам нужно создание, значит это первый коммит (в списке последний). Отрезаем последнюю строчку (tail -n 1).
```
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git log -SproviderSource --oneline | tail -n 1
5e06e39fcc Use registry alias to fetch providers
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ 
```

 * >Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.

```
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git log -SglobalPluginDirs --oneline
65c4ba7363 Remove terraform binary
125eb51dc4 Remove accidentally-committed binary
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a Don't show data while input if sensitive
35a058fb3d main: configure credentials from the CLI config file
c0b1761096 prevent log output during init
8364383c35 Push plugin discovery down into command package
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ 
```

 * >Кто автор функции `synchronizedWriters`? 
Сначала ищем первый коммит (в списке последний) по указанному запросу, а потом делаем git show на его хеш.
В резльтате получаем автор Martin Atkins <mart@degeneration.co.uk>
```
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git log -SsynchronizedWriters --oneline | tail -n 1
5ac311e2a9 main: synchronize writes to VT100-faker on Windows
seregin@msk-s3-arm076:~/scripts/edu/git4/terraform$ git show 5ac311e2a9
commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Wed May 3 16:25:41 2017 -0700
```

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
