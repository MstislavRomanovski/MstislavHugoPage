---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Контроль версий GIT"
subtitle: "История о том как я контроль версий GIT осваивал"
summary: ""
authors: [Мальков Роман Сергеевич]
tags: []
categories: []
date: 2022-05-07T13:46:18+03:00
lastmod: 2022-05-07T13:46:18+03:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---
# Этапы работы
* Создать базовую конфигурацию для работы с git.
* Создать ключ SSH.
* Создать ключ PGP.
* Настроить подписи git.
* Зарегистрироваться на Github.
* Создать локальный каталог для выполнения заданий по предмету.

# Выполнение
Создаем учётную запись на https://github.com и заполняем нужные данные(Скриншот 1).
![Screenshot_1](/gitcontrol/screens/Screenshot_1.png)

( Скриншот 1 )

Устанавливаем git-flow и gh на Fedora Linux(Скриншот 2-3), используя следующие команды.

```
cd /tmp
2 wget --no-check-certificate -q https://raw.github.com/petervanderdoes ⌋
↪ /gitflow/develop/contrib/gitflow-installer.sh
3 chmod +x gitflow-installer.sh
4 sudo ./gitflow-installer.sh install stable
sudo dnf install gh
```

![Screenshot_2](/gitcontrol/screens/Screenshot_2.png)
(Скриншот 2)

![Screenshot_22](/gitcontrol/screens/Screenshot_22.png)
(Скриншот 3)

Производим базовую настроуку git, задаем имя и електронную почту владельца репозитория(Скриншот 4):
```
git config --global user.name "Name Surname"
2 git config --global user.email "work@mail"
```
Настраиваем utf-8 в выводе сообщений git(Скриншот 4):

```
git config --global core.quotepath false
```
![Screenshot_4](/gitcontrol/screens/Screenshot_4.png)
(Скриншот 4)
Настраиваем верефикацию и подписание git, задаем имя начальной ветки, задаем параметр autocrlf и  safecrlf(Скриншот 5):
```
git config --global init.defaultBranch master
git config --global core.autocrlf input
git config --global core.safecrlf warn
```

![Screenshot_3](/gitcontrol/screens/Screenshot_3.png)
(Скриншот 5)

Создаем ключи ssh по алгоритму rsa размером 4096, и по алгоритму ed25519(Скриншот 6-7):

```
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519
```
![Screenshot_5](/gitcontrol/screens/Screenshot_5.png)
(Скриншот 6)
![Screenshot_6](/gitcontrol/screens/Screenshot_6.png)
(Скриншот 7)

Создаем ключ pgp(Скриншот 8):
```
gpg --full-generate-key
```
* Из предложенных опций выбираем:
* тип RSA and RSA;
* размер 4096;
* выберите срок действия; значение по умолчанию— 0 (срок действия не истекает
никогда).
* GPG запросит личную информацию, которая сохранится в ключе:
* Имя (не менее 5 символов).
* Адрес электронной почты.
* При вводе email убедитесь, что он соответствует адресу, используемому на
GitHub.
* Комментарий. Можно ввести что угодно или нажать клавишу ввода, чтобы
оставить это поле пустым.

![Screenshot_7](/gitcontrol/screens/Screenshot_7.png)
(Скриншот 8)

Далее копируем отпечаток привтаного ключа, он выводился на экран консоли, при генерации(Скриншот 9).

![Screenshot_8](/gitcontrol/screens/Screenshot_8.png)
(Скриншот 9)

После этого, используем команду указанную ниже, чтобу получить ключ, и ввести его на https://github.com/settings/keys (Скриншот 10):

![Screenshot_9](/gitcontrol/screens/Screenshot_9.png)
(Скриншот 10)
```
gpg --armor --export <Ваш отпечаток приватного ключа>
```
Настраиваем автоматические подписи git(Скриншот 11):

```
git config --global user.signingkey <PGP Fingerprint>
2 git config --global commit.gpgsign true
3 git config --global gpg.program $(which gpg2)
```

![Screenshot_10](/gitcontrol/screens/Screenshot_10.png)
(Скриншот 11)

Настройка gh(Скриншот 12):
```
gh auth login
```
![Screenshot_11](/gitcontrol/screens/Screenshot_11.png)
(Скриншот 12)

Создаем репозиторий курса на основе шаблона(Скриншот 13-15):
```
mkdir -p ~/work/study/2021-2022/"Операционные системы"
2 cd ~/work/study/2021-2022/"Операционные системы"
3 gh repo create study_2021-2022_os-intro
↪ --template=yamadharma/course-directory-student-template --public
4 git clone --recursive
↪ https://github.com/MstislavRomanovski/study_2021-2022_os-intro.git
```

![Screenshot_12](/gitcontrol/screens/Screenshot_12.png)
(Скриншот 13)
![Screenshot_13](/gitcontrol/screens/Screenshot_13.png)
(Скриншот 14)
![Screenshot_14](/gitcontrol/screens/Screenshot_14.png)
(Скриншот 15)

Настраиваем каталог курса, а имеено, переходим в каталог курса, удаляем лишние файлы(у меня не удалились), созадем необходимые каталоги(пришлось получить рут права для этого), и отправляем файлы на сервер(Скриншоты 16-20):
```
cd ~/work/study/2021-2022/"Operating Systems"/study_2021-2022_os-intro
rm package.json
make COURSE=os-intro
git add .
git commit -am 'feat(main): make course structure'
git push
```
![Screenshot_16](/gitcontrol/screens/Screenshot_16.png)
![Screenshot_18](/gitcontrol/screens/Screenshot_18.png)
![Screenshot_19](/gitcontrol/screens/Screenshot_19.png)
![Screenshot_20](/gitcontrol/screens/Screenshot_20.png)
![Screenshot_21](/gitcontrol/screens/Screenshot_21.png)
(Скриншоты 16 - 20)