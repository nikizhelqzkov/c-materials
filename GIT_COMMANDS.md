
## Създаване на Git Repository

* Създаване на папка и няколко файла (наличен проект)
* `git init` в папката
* `git add .` + `git commit`
* Създаване на repository в GitHub.
* `git remote add origin https://github.com/AGalabov/Test-git.git` - без SSH,
* `git remote add origin git@github.com:AGalabov/Test-git.git` - със SSH
* `git remote set-url origin git@github.com:AGalabov/Test-git.git` - ако се наложи да се смени
* `git push -u origin master`
* име и парола за акаунта

## Конфигурация на Git Repository

* `git config --local user.email [email]`
* `git config --local user.name [username]`
* `git config --local -l`

## Работа по съществуващо repository

* Fork - създава се копие на проект (repository) в персонален GitHub
* `git clone <repository>` - създава се локално копие (сваля се) съдържанието от remote repository-то на машина

## Добавяне на SSH ключ

* `ssh-keygen -t rsa -C "alexandar_1997@abv.bg"` - създава SSH ключ
* `ssh-add -l` - наличните ключове
* `cat ~/.ssh/id_rsa.pub` - съдържанието на ключа в случай, че не му е сменяно името по време на генерирането
* В GitHub Settings -> SSH and GPG keys -> New SSH key
* копира се съдържанието на ключа и се дава някакво име
* `ssh -T git@github.com` - ако всичко е наред ще изпише *"Hi, username ..."*

## Основни команди за работа с локални промени

* `git status` - показва текущото локално състояние - промени, които още не са commit-нати. Разделят се на **staged**, **not stage**, **untracked**.
* `git add <file(s)>` - **stage**-ване на файл. (само за файлове, които са **not staged** или **untracked**)
* `git checkout <file(s)>` - **unstage**-ване на файл (само за файлове, които са **staged**)
* `git commit` - прави се commit с промените досега (всички stage-нати промени) като му се дава име
* `git push` - локалните промени (които преди това са commit-нати) се push-ват в remote repository-то (примерно GitHub), така че да може да се достъпва от други хора.
* `git stash` - запазва всички текущи промени локално
* `git stash pop` - "връща" последните **stash**-нати неща 

## Основни команди за работа с бранчове

* `git branch <branch_name>` - създава нов branch(разклонение) от текущият 
* `git checkout <branch_name>` - мести на избрания бранч
* `git checkout -b <branch_name>` - комбинация на горните 2 - създава нов бранч от текущия и мести на него
* `git fetch <remote>` - сваля remote (от repository-то) файловете локално. Пазейки ги локално не е нужно постоянно да се пита сървъра за наличие на промени.
* `git merge <branch_name>` - обединява указаният branch с текущия. Обединява двете "истории" 
* `git pull` = `git fetch <remote>` + `git merge`

## Какво има в папката .git

* `tree .git` - наличието на `.git/` е единствената разлика с обикновена папка

### За .git/objects
* `git cat-file -t [folder][object]` - показва типа на обекта -> **blob**, **tree**, **commit**.
* `git cat-file -p [folder][object]` - показва съдържанието на обекта
* *Наблюдения:* **blob** = файл, **tree** = папка, **commit** - "връзка" между обекти. Има собствен **tree** обект, *поне един* **parent** обект и пази информация за къмита - автор, timestamp, message. Историята на git е DAG (Ориентиран граф без цикли).
* `git log` - хваща последният къмит и проследява parent връзките.

### За .git/HEAD
* `cat .get/HEAD` - HEAD e просто файл, пазещ името на branch, което е път към файл
* `cat .git/refs/heads/<branch_name>` - е файл, който пази обект. Ако проследим този обект ще разберем, че той е commit.

### За .git/index
* виртуална папка, която да пази нещата за **stage** - тези, които ще **commit**-нем със следващият **commit**.
* `git ls-files --stage` - показва локланите файловете (като snapshot). За сравнение `git status` показва само промените.



