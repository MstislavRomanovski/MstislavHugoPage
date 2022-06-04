---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Git version control"
subtitle: "Mys story about learning GitHub"
summary: ""
authors: [Malkov Roman Sergeevich]
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
# Stages of work
* Create a basic configuration for working with git.
* Create an SSH key.
* Create a PGP key.
* Set up git signatures.
* Sign up on Github.
* Create a local directory for completing assignments on the subject.

# Performance
Create an account on https://github.com and fill in the required data (Screenshot 1).
![Screenshot_1](/gitcontrol/screens/Screenshot_1.png)

( Screenshot 1 )

Install git-flow and gh on Fedora Linux (Screenshot 2-3) using the following commands.

```
cd /tmp
2 wget --no-check-certificate -q https://raw.github.com/petervanderdoes ⌋
↪ /gitflow/develop/contrib/gitflow-installer.sh
3 chmod +x gitflow-installer.sh
4 sudo ./gitflow-installer.sh install stable
sudo dnf install gh
```

![Screenshot_2](/gitcontrol/screens/Screenshot_2.png)
(Screenshot 2)

![Screenshot_22](/gitcontrol/screens/Screenshot_22.png)
(Screenshot 3)

We make a basic git setup, set the name and email of the owner of the repository (Screenshot 4):
```
git config --global user.name "Name Surname"
2 git config --global user.email "work@mail"
```
Set up utf-8 in git output (Screenshot 4):

```
git config --global core.quotepath false
```
![Screenshot_4](/gitcontrol/screens/Screenshot_4.png)
(Screenshot 4)
Set up git verification and signing, set the name of the initial branch, set the autocrlf and safecrlf parameters (Screenshot 5):
```
git config --global init.defaultBranch master
git config --global core.autocrlf input
git config --global core.safecrlf warn
```

![Screenshot_3](/gitcontrol/screens/Screenshot_3.png)
(Screenshot 5)

We create ssh keys using the rsa algorithm with a size of 4096, and using the ed25519 algorithm (Screenshot 6-7):

```
ssh-keygen -t rsa -b 4096
ssh-keygen -t ed25519
```
![Screenshot_5](/gitcontrol/screens/Screenshot_5.png)
(Screenshot 6)
![Screenshot_6](/gitcontrol/screens/Screenshot_6.png)
(Screenshot 7)

Create a pgp key (Screenshot 8):
```
gpg --full-generate-key
```
* From the proposed options, choose:
* type RSA and RSA;
* size 4096;
* select the expiration date; default value is 0 (does not expire
never).
* GPG will ask for personal information, which will be stored in the key:
* Name (at least 5 characters).
* E-mail address.
* When entering an email, make sure it matches the address used on
GitHub.
* Comment. You can type anything or press the enter key to
leave this field blank.

![Screenshot_7](/gitcontrol/screens/Screenshot_7.png)
(Screenshot 8)

Next, we copy the fingerprint of the private key, it was displayed on the console screen during generation (Screenshot 9).
![Screenshot_8](/gitcontrol/screens/Screenshot_8.png)
(Screenshot 9)

After that, use the command below to get the key and enter it on https://github.com/settings/keys (Screenshot 10):

![Screenshot_9](/gitcontrol/screens/Screenshot_9.png)
(Screenshot 10)
```
gpg --armor --export <your private key fingerprint>
```
Set up automatic git signatures (Screenshot 11):

```
git config --global user.signingkey <PGP Fingerprint>
2 git config --global commit.gpgsign true
3 git config --global gpg.program $(which gpg2)
```

![Screenshot_10](/gitcontrol/screens/Screenshot_10.png)
(Screenshot 11)

Setting gh (Screenshot 12):
```
gh auth login
```
![Screenshot_11](/gitcontrol/screens/Screenshot_11.png)
(Screenshot 12)

Create a course repository based on the template (Screenshot 13-15):
```
mkdir -p ~/work/study/2021-2022/"Operating Systems"
2 cd ~/work/study/2021-2022/"Operating systems"
3 gh repo create study_2021-2022_os-intro
↪ --template=yamadharma/course-directory-student-template --public
4 git clone --recursive
↪ https://github.com/MstislavRomanovski/study_2021-2022_os-intro.git
```

![Screenshot_12](/gitcontrol/screens/Screenshot_12.png)
(Screenshot 13)
![Screenshot_13](/gitcontrol/screens/Screenshot_13.png)
(Screenshot 14)
![Screenshot_14](/gitcontrol/screens/Screenshot_14.png)
(Screenshot 15)

We set up the course directory, and yes, go to the course directory, delete unnecessary files (I didn’t delete them), create the necessary directories (I had to get root rights for this), and send the files to the server (Screenshots 16-20):
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
(Screenshots 16 - 20)