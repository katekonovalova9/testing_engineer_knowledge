# 1. VCS concept

- хранение в папках - 1 уровень ( сложно для понимания где какая версия)
- пошарить папку по сети - 2 уровень ( делиться с другим разработчиком, одновременно нельзя править файл, будет перезапись)
- облачные хранилища - 3 уровень (синхронизация будет проблемой)

Система версионного контроля (VCS) , что должна уметь: 
1) backup and restore - иметь возможность создавать резервную копию 
2) synchronization - синхронизация нескольких разработчиков одновременная работа
3) undo - возможность отмены каких-то изменений
4) track changes and ownership - возможность отслеживания изменений и их авторов
5) sandboxing - возможность создания песочниц (где можно попробовать что-то новое, эксперимент)
6) branching - возможность создания веток и их слияние

 Системы контроля версий можно поделить на несколько категорий по механизму их взаимодействия с файлами: 
 1 - Lock-modify-unlock (SCCS, VAULT)
 2 - Copy-modify-merge (CVS, Git, Mercurial, GNU bazaar)
 
# 2. Version control types
 
## Lock-modify-unlock strategy 
для внесения правок файла, надо его заблокировать, и исправить, далее выложить и снять блокировку, чтобы смогли править другие пользователи. Перед тем как править надо подтянуть изменения в свою локальную копию

## Copy-modify-merge strategy 
нет возможности заблокировать файл, все правят файл в любое время, подтягивает изменения с сервера и при этом остаются новые изменения. 

## Centralized vs Distributed
Цетральная - есть сервер с базой версий и клиент
Распределенная - есть сервер с базой версий и у каждого из пользователей есть репозиторий свой, с базой версий, то есть каждый может быть сервером

# 3. Why Git
гит был в 2005 году сделан
открытый исходный код
быстрее других происходят операции
гарантия сохранности и целостности данных
делает snapshot файла хэш-функцией
можно делать много веток

# 4. Download, install, configure
скачать и установить гит

генерация ключей
$ssh-keygen -t rsa -C "user@mail.ru"

Публичный ключ (id_rsa) нужно отправить владельцу репозитория для получения прав работы. Или загрузить в настройки профиля в bitbucket/github/gitlab
на гитхабе в настройках -> ssh and GPG keys добавить ключ public

сконфигурировать username и email
git config --global user.name "vitali"
git config --global user.email "vitail@mail.ru"

# 5. Create a github repo and clone it
git clone git@github.com:https://github.com/katekonovalova9/testing_engineer_knowledge.git

git remote -v

добавление файла: 
git status
git add song.txt
git status
git commit -m "add"
сначала добавляем файлы через add, потом делаем коммит и синхронизируем локальный репозиторий с удаленным через git push.

git log - посмотреть историю коммитов

git push - синхронизация локального с удаленным репозиторием

# 6. Pull from remore
подтянуть изменения с удаленного репозитория в локальный

git fetch - синхронизация удаленного и локального (потом нужен merge)

git pull заменяет предыдущие две, чтобя подтянуть изменения

# 7. Git GUI and gitk

git gui& запуск интерфейса

# 8. Inside .git folder
git show -s 
git ls-tree
git show

# 9. Undoing changes - отменить изменения
git status

Working directory
  git checkout -- file.txt
  git checkout - вернуть состояние файла до изменения
  git clean -xdf  - удаляет новый файл
  
Staging area (Index)
  git reset -- file.txt

local branch - удалить коммит 
  git reset HEAD^^ (HEAD~2) - какое число коммитов назад надо удалить
  git commit --amend -m "commit message"
  
Remote repository
  git revert <sha1>
 

# 10. Git reset
git reset --soft
git reset --mixed
git reset --hard

# 11. Git revert
отменять изменения которые закомитили и запушили на github

# 12. .gitignore
позволяет отфильтровать сообщения о изменениях

no .log files
*.log

but do track error.log, even though you are ignoring .log files above
!error.log

only ignore the TODO file in the current directory, no subdir/TODO
/TODO

ignore all files in the build/ directory
build/

ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

ignore all .pdf files in the doc/ directory
doc/**/*.pdf

# 13. Branching and merge
можно создавать ветки от мастера 
merge - слияние : 
- fast-forward merge перемотка
- non fast-forward merge

# 14. Conflict solving
разрешение конфликтов

# 15. Rebase 

# 16. Cherry-pick 
взять коммит из одной ветки и поместить в другую ветку

# 17. Tags 

Mark commit with tag
  git tag ver1

View tags
  git tag -list
  
Push
  git push --tags

Check it out
  git checkout ver1
  
# 18. Stashing
сохранить свою работу во временное хранилище которое не закомичено

Save working directory 
  git stash save "description"

View stashes
  git stash list
  
Bring them back
  git stash pop (and remove from stash)
  git stash apply (leave in stash)

Remove
  git stash drop (clear)
  
# 19. Remotes

Add
  git remote add <name> <url>
  git remote add origin git@github.com:user/repo
  
View
  git remote -v
  git remote show <name>
  
# 20. Branching strategies

1 - Centralized strategy есть одна ветка на которую коммитят
2 - Feature-branch workflow есть другие ветки от мастера
3 - Gitflow
4 - 

# 21. Extras

book :
 - Git book 
 - Version Control with Git, 2nd Edition O'Reilly
 
 git config --global user.name "kate"
 git blame посмотреть кто редактировал файл
 git bisect бинарный поиск
 git log --pretty=oneline красивый вывод консоля
 git last
 git rerere
 git submodule
 
Презентация треннинга - https://elearn.epam.com/assets/courseware/v1/d8b3970d06d567a94e0bb179b8d84acb/asset-v1:EPAM+VCG+RU+type@asset+block/DevTestOps-Version_Control_with_Git.pdf

Официальный сайт Git: https://git-scm.com/

Книга "ProGit", второе издание, на русском: https://git-scm.com/book/ru/v2


# Практические задания

## 1. I Can Win 

1. Установите git и сгенерируйте пару ssh ключей. Авторизуйте публичный ключ на github.com.
2. Укажите свой user.name и user.email в git.
3. Создайте новый репозиторий на github.com и склонируйте его локально на свой компьютер.
4. Создайте файл названием song.txt и поместите туда половину текста любимой песни.
5. Сделайте коммит с названием "add first half of my favorite song" и отправьте его на сервер.
6. Убедитесь что на github есть файл song.txt с текстом песни.
7. Используя веб-интерфейс гитхаба добавьте вторую половину текста песни и сделайте коммит с названием "finish my song".
8. В локальном репозитории сделайте pull и убедитесь что коммит, который вы создали на github, подтянулся и у вас полный текст песни.
