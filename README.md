---
title: "Программа обучающего курса по Git"
author: Valeriy Osipov
presentation:
  enableSpeakerNotes: true
---
<!-- slide -->

## О данном курсе

- По Git, как и по другим IT-технологиям, есть море различных ресурсов.
- Особенностью данного курса является то, что выделены основные варианты использования Git'а. И показано как все эти варианты использования реализуются в основных инструментах:
  - Shell
  - текстовый редактор VSCode
  - IDE PHPStorm и
  - GUI для Git'а Sourcetree
- Это позволит выполнять все действия с Git в вашем основном инструменте, что будет препятствовать потере фокуса и будет способствовать повышению продуктивности
<!-- slide -->

## Что такое Git

- Git - это распределённая система управления версиями
- Git - это некий аналог блокчейн
- Альтернативой Git может выступать, например, Mercurial

<!-- slide -->
## Назначение Git

- Хранение исходного кода <!-- .element: class="fragment" data-fragment-index="1" -->
- Развертывание <!-- .element: class="fragment" data-fragment-index="2" -->
<!-- slide data-notes="Настройка различных инструментов для работы с Git" -->

## Git инструментарий

- Shell:
  - Cmder: PowerShell: Posh-Git: Установка: запустить PowerShell с правами администратора и выполнить: "Install-Module posh-git"
- VSCode:
  - [Cmder & VS Code Integration](https://github.com/cmderdev/cmder/wiki/Seamless-VS-Code-Integration)
  - `Git Extension Pack` by Don Jayamanne:
    - Минусы: Отсутствует [`gitflow`](https://marketplace.visualstudio.com/items?itemName=vector-of-bool.gitflow), `Git Merger`
- PHPStorm:
  - Settings | Tools | Terminal | `"cmd.exe" /k "<path_to_cmder>\vendor\init.bat"`
- GitLab, SourceTree:
  - ничего настраивать не нужно
<!-- slide -->

## Основные варианты использования
<!-- slide  -->

### Установка Git

- [Страница загрузки на официальном сайте](https://git-scm.com/download/win)
- SourceTree:
  - Sourcetree при установке может устанавливать git и hg
- Windows Server:
  - Web Platform Installer (WebPI): Git for Windows присутствует в WebPI
<!-- slide -->

### Инициализация Git репозитория

- Shell: `git init`
- VSCode: `Git: Initialize Repository`
- PHPStorm: VCS | Import into Version Control | Create Git Repository...
- Sourcetree: New tab | Create
<!-- slide -->

### Игнорирование файлов

- VSCode: [`gitignore` extension](https://github.com/CodeZombieCH/vscode-gitignore):
  - Простое расширение для Visual Studio Code, которое позволяет pull'ить `.gitignore` файлы из [репозитоия](https://github.com/github/gitignore). Добавляется команда `Add gitignore` с поддержкой шаблонов - как в плагине `.ignore` в PHPStorm
  - Минусы:
    - При добавлении какого-либо шаблона в `.gitignore` несколько раз он добавляет несколько копий, хотя дублировать не нужно - в отличие от PyCharm
    - Это расширение позволяет добавлять в `.gitignore` только файлы, но не позволяет добавлять в `.gitignore` директории - в отличие от `.ignore` плагина для PHPStorm
  - Плюсы:
    - включен в `Git Extension Pack`
<!-- slide -->

### Игнорирование файлов #2

- PHPStorm: плагин [`.ignore`](https://github.com/hsz/idea-gitignore):
  - Плюсы: подчеркивает entries defined more than one - в отличие от `gitignore` расширение в VSCode
- Sourcetree:
  - In Sourcetree you should be able to right click on one of the files/folders and select `ignore`. This will auto create a `.gitignore` file for you with that particular file/folder in it
  - Options | Git | Global Ignore List
  - Минусы: нет шаблонов - в отличие от расширения `gitignore` в VSCode, `.ignore` плагин в PHPStorm
<!-- slide -->

### Работа с ветками
<!-- slide vertical=true -->

#### Что такое ветка в Git

Ветка в Git - это метка для коммита. The label moves to new commits as they are created. Когда вы содаете новую ветку вы ничего не изменяете в структуре репозитория. Вы просто создаете новую метку

В Git есть два типа веток:

- Локальные ветки - хранятся в директории .git/refs/heads/
- Удаленные (Remote-tracking) ветки
<!-- slide vertical=true -->

#### View branch list. List of branches

- Shell:
  - Local branches: `git branch`
  - Remote branches: `git branch -r`
- VSCode: кликнуть на текущей ветке в левом нижнем углу. Появится меню со списком веток
- PHPStorm: кликнуть на текущей ветке в правом нижнем углу. Появится меню со списком веток
- Sourcetree: список веток отобажается в левом sidebar'е в узле "BRANCHES"
<!-- slide vertical=true -->

#### Создание новой ветки

- Shell: `git branch <branch_name>`
- VSCode:
  - кликнуть на текущей ветке в левом нижнем углу. Появится меню с пунктами `Create new branch...` и `Create new branch from...`. При выборе пункта `Create new branch...` после создания ветки происходит checkout в эту ветку
  - `Git: Create Branch From...`, `Git: Create Branch`
  - [`Git Lens`](https://github.com/eamodio/vscode-gitlens): Branch Context menu | `Create Branch (via Terminal)...`
- PHPStorm:
  - кликнуть на текущей ветке в правом нижнем углу. Появится меню с пунктом "New Branch"
  - При подключении JIRA в качестве Issue Tracker'а при открытии задачи есть галка `Create branch`
- Sourcetree: Repository | Branch | New Branch
<!-- slide vertical=true -->

#### Узнать какая ветка текущая

- Shell:
  - В Cmder & Posh-Git текущая ветка отображается в приглашении консоли. Но следует помнить, что это значение не изменяется при изменении текущей ветки иными способами
  - `git status`
- VSCode: текущая ветка отображается в левом нижнем углу
- PHPStorm: текущая ветка отображается в правом нижнем углу
- Sourcetree: текущая ветка выделена жирным шрифтом
<!-- slide vertical=true -->

#### Checkout branch
<!-- slide vertical=true -->

##### Checkout branch during create

- Shell: `git checkout -b feature` - Создаёт новую ветку, названную `feature` и делает её активной
- VSCode:
  - `Git: Create Branch`: после создания ветки происходит checkout в эту ветку
  - кликнуть на текущей ветке в левом нижнем углу. Появится меню с пунктами `Create new branch...` и `Create new branch from...`. При выборе пункта `Create new branch...` после создания ветки происходит checkout в эту ветку
- PHPStorm: кликнуть на текущей ветке в правом нижнем углу. Появится меню с пунктом "New Branch". В окне "Create New Branch" есть галка "Checkout branch"
- Sourcetree: Repository | Branch | New Branch. Есть галка "Checkout New Branch"
<!-- slide vertical=true -->

##### Checkout branch after create

- Shell: `git checkout <branch_name>`
- VS Code:
  - Можно кликнуть на названии ветки в левом нижнем углу и выбрать из меню новую ветку
  - `Git: Checkout to...` command
  - [`Git Lens`](https://github.com/eamodio/vscode-gitlens):
    - Branch Context menu | `Checkout`
    - справа от названия ветки есть конка "Checkout"
  - Минусы: При переключении ветки в VS Code текущая ветка в Cmder не изменяется
- PHPStorm:
  - переключатель веток находится в правом нижнем углу, в строке состояния
  - Минусы: При переключении ветки в VS Code текущая ветка в Cmder не изменяется
- SourceTree:
  - двойной клик на ветке
  - Main menu | Repository | Checkout...
  - SourceTree при переключении веток переключает их со всеми изменениями, не перенося изменения в stash
<!-- slide vertical=true -->

#### Удалить локальную ветку

- Shell:
  - `git branch -d <branch_name>`
  - `git branch -D <branch_name>`
- VS Code:
  - `Git: Delete Branch...`. Эта команда удаляет только локальные ветки. Удалить с помощью этой команды удаленные (remote) ветки нельзя
  - [`Git Lens`](https://github.com/eamodio/vscode-gitlens): Branch Context menu | `Delete Branch (via Terminal)`. Этот способ для remote branches не работает
- PHPStorm: кликнуть на текущей ветке в правом нижнем углу. Появится меню со списком веток. Кликнуть на стрелочку справа от ветки. В открывшемся меню выбрать "Delete"
- Sourcetree:
  - from context menu: "Delete <branch_name>..."
  - Main menu | Repository | Branch | Delete Branches
  - при выполнении "Git-flow | Finish Feature" в окне "Finish Feature" есть галки "Delete branch" и "Force deletion"
<!-- slide vertical=true -->

#### Переименовать ветку

- Shell: `git branch -m old_branch new_branch`
- VSCode: `Git: Rename Branch...` - переименовывает текущую ветку
- PHPStorm: кликнуть по стрелочке справа от имени branch'а и появится "Rename..."
- Sourcetree: Branch context menu: "Rename <branch_name>..."
- GitLab: [Cannot rename branches](https://gitlab.com/gitlab-org/gitlab-ce/issues/50840)
<!-- slide vertical=true -->

#### Сравнить две ветки

- Shell:
  - `git diff branch1 branch2`
- VSCode:
  - Git Lens: `COMPARE` node
  - [`GitLab Workflow`](https://gitlab.com/fatihacet/gitlab-vscode-extension):
    - `GitLab: Compare current branch with master` - открывает сравнение веток в GitLab'е
- PHPStorm:
  - Git | Compare with branch - сравнивает один файл
  - Выбрать ветку (либо Context menu | Git | Repository | Branches | \<choose branch\>, либо кликнуть на текущей ветке в правом нижнем углу), кликнуть по стрелочке справа от ветки и выбрать "Compare with Current" - сравнивает все файлы в ветке
- Sourcetree:
  - щелкнуть правой кнопкой мыши на ветке и выберать из контекстного меню пункт "Diff against current" (current refers to the branch you are currently working on). This will give you the diff between the head commits of the two branches
<!-- slide vertical=true -->

#### Работа с удаленными (Remote-tracking) ветками
<!-- slide vertical=true -->

##### Pulling

- Shell:
  - `git pull`
  - `git pull origin <branch>`
- VSCode:
  - `Git: Pull`
  - `Git: Pull from...`
- PHPStorm:
  - `Update Project (update project)` кнопка на панели инструментов
  - Main menu | VCS | Update Project...
  - Main menu | VCS | Git | Pull...
- Sourcetree:
  - `Pull` кнопка на панели инструментов
  - Branch Context menu | Pull (tracked)
<!-- slide vertical=true -->

##### Pushing

- Shell:
  - `git push`
  - `git pull origin <branch>`
- VSCode:
  - `Git: Push`
  - `Git: Push to...`
- PHPStorm:
  - Main menu | VCS | Git | Push...
  - в окне "Commit Changes" если нажать на стрелочку справа от кнопки "Commit", то появится кнопка "Commit and Push..."
- Sourcetree:
  - `Push` кнопка на панели инструментов
  - Branch Context menu | `Push to`, `Push to (tracked)`
  - Плюсы: Sourcetree позволяет пушить сразу несколько веток - в отличие от PHPStrom
<!-- slide vertical=true -->

#### Слияние

- Shell:
  - `git merge`
- VS Code:
  - `Git: Merge Branch...`
  - расширение `Git Merger`:
    - Минусы: missed in the `Git Extension Pack`
- PHPStorm:
  - кликнуть на текущей ветке в правом нижнем углу), кликнуть по стрелочке справа от ветки и выбрать `Merge into Current`
- Sourcetree:
  - Branch context menu | Merge <branch_name> into current branch
<!-- slide vertical=true data-notes=" -->

##### Разрешение базовых конфликтов слияния

- Shell:
    Merge conflicts occur when the same part of the code has been modified in both branches. For example, if the same line of `README.md` is edited in `fix` and `master`. The file impacted will have conflict-resolution markers (`<<<<<<<` and `>>>>>>>`) added to it by git, showing the conflicting lines (separated by `=======`)

    ```shell
    $ git merge fix
    # conflict with README.md
    # merge failed
    $ cat README.md
    To contact us email:
    <<<<<<< HEAD
    hello@enki.com
    =======
    help@enki.com
    >>>>>>> fix
    ```

    You have to manually choose the option you want or combine them. Then run `git add` to mark the file as resolved. When you're done resolving conflicts finalize the merge with `git commit`
<!-- slide vertical=true -->

##### Разрешение базовых клнфликтов слияния #2

- VSCode:
  - Нажать на кнопку "Source Control" слева
  - See MERGE CHANGES in sidebar.
  - Those files have merge conflicts.
- PHPStorm: "Resolve Conflicts"
- Sourcetree: Main menu | Actions | Resolve Conflicts
<!-- slide -->

### Работа с коммитами
<!-- slide vertical=true -->

#### Создание коммита

- Shell: `git commit -m <commit_message>`
- VSCode:
  - `Git: Commit`, `Git: Commit All`
  - нажать на кнопку "Source Control". В открывшемся sidebar'е есть сверху кнопка "Commit"
- PHPStorm:
  - кнопка Commit на панели инструментов
  - Main menu| VCS | Commit
- Sourcetree:
  - Нажать на кнопку "Commit" на панели инструментов
  - В окне "Unstaged files" содержатся все непроиндексированные изменения. Выберать файлы для индексации перед коммитом
  - В окне "Staged files" содержатся все проиндексированные файлы. Для удаления файла из индекса нажать на "минус" справа от файла
  - Ввести комментарий к коммиту
  - Нажать кнопку "Commit" для фиксации всех проиндексированных изменений в репозитории
<!-- slide vertical=true -->

#### Partial commits

- VS Code: `Git: Stage Selected Ranges`
- PHPStorm: в окне "Commit Changes" можно галочками выбирать изменения
- Sourcetree: WORKSPACE | File Status: you can select lines to stage in the diff view of each uncommitted file. Then you commit what is in staging
<!-- slide vertical=true data-notes="Cherry-picking is the method to apply a single, specific commit from another branch. This is most useful when you are unable to merge the two branches. For example, you might want to fix a security issue present in both branches"-->

#### Cherry-pick

- Shell:

    ```shell
    $ git checkout master
    $ git cherry-pick a456bd7
    # merge commit a456bd7 (from another branch)
    # with branch master
    ```

- VSCode: [`Git History`](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory):
  - `Cherrypick into current branch`: Сначала необходимо выбрать коммит в `Git History`
  - Context menu | Git: View File History. В открывшемся окне "File History" справа от каждого коммита есть кнопка "Cherry pick, Compare, etc"
- PHPStorm: Version Control window | Log tab | commit context menu | Cherry-Pick
- SourceTree: In the log view (Cmd-2), just select one or more commit lines (Cmd-click or Shift-click multi-selects), then right-click and select 'Cherry pick'
<!-- slide vertical=true -->

#### Amend commit (change your most recent commit)

- Shell:

    To make changes to your most recent commit use: `$ git commit --amend`
    For example, you might want to edit the name of the commit:

    ```shell
    $ git commit -m 'my first comit'
    $ git commit --amend
    # editor opens
    'my first commit'
    ```

- VSCode: `Git: Commit All (Amend)`, `Git: Commit Staged (Amend)`
- PHPStorm: в окне "Commit Changes" есть галка "Amend commit"
- Sourcetree: In SourceTree, the “Commit options…” dropdown list to the right of the commit dialog has an option to “Amend latest commit.” You’ll be asked if you want to replace the commit text in your current dialog with the message of the previous commit. Say yes, since you’re adding a file to the previous commit that you had meant to include all along
<!-- slide vertical=true -->

#### Revert commit

This generates a new commit with all the changes introduced in \<commit\> afterwards applying it to the current branch

- Shell:
  - `git revert <commit>`.
- VSCode:
  - [`Git History`](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory):
  - Context menu | Git: View File History. В открывшемся окне "File History" справа от каждого коммита есть кнопка "Cherry pick, Compare, etc". В открывшемся меню есть пункт "Revert this (...) commit"
- PHPStorm:
  - VCS | Git | Revert...
  - кнопка "Revert" на панели инструментов
- Sourcetree:
  - Commit context menu | Reverse commit...
<!-- slide -->

## Git Flow diagram

![Git Flow diagram](git-model@2x.png)

<!-- slide -->

## Git Flow Tools

- Shell
- VSCode: [расширение `gitflow`](https://marketplace.visualstudio.com/items?itemName=vector-of-bool.gitflow):
  - `GitFlow: Initialize repository for gitflow` - создает бранчи `develop` и `master` - в отличие от `Git-flow` button from `Sourcetree`
- PHPStorm:
  - [плагин `Git Flow Integration`](https://plugins.jetbrains.com/plugin/7315-git-flow-integration)
  - При подключении JIRA в качестве Issue Tracker'а при открытии задачи есть галка `Create branch`
- Sourcetree:
  - Main menu | Repository | Git-flow | Initialise repository
  - `Git-flow` button:
    - Не создает автоматически бранчи - в отличие от `GitFlow: Initialize repository for gitflow` в VSCode

<!-- slide -->

## Практические задания
<!-- slide -->

### Настроить рабочее окружение

1. Установить Git и настроить свой любимый инструмент для работы с Git
2. Склонировать учебный репозиторий из GitLab
3. Проверить состояние репозитория (`git status`), определить какие есть ветки и какая ветка текущая
<!-- slide -->
### Создать новый файл и закоммитить его

<!-- slide -->
### Создать feature-branch

1. Создать feature-ветку от `develop`
2. Внести изменения в определенную строчку определенного файла
3. Закоммитить изменения
4. Сравнить текущую ветку с `develop`

<!-- slide -->
### Создать конфликт при слиянии изменений

1. Переключиться на ветку `develop`
2. Внести другие изменения в ту же строчку того же файла. Закоммитить изменения
3. Попробовать смерджить feature-ветку
4. Разрешить конфликт

<!-- slide -->
### Посмотреть историю изменений

`git log`

<!-- slide -->
### Запушить ветку на remote

в GitLab

<!-- slide -->
### Создать Merge Request