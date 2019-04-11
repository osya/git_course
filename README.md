# Программа обучающего курса по Git

## Что такое Git

- Git - это распределённая система управления версиями
- Git - это некий аналог блокчейн
- Альтернативой Git может выступать, например, Mercurial

## Назначение Git

- Хранение исходного кода
- Развертывание

## О данном курсе

По Git, как и по другим IT-технологиям, есть море различных ресурсов. Особенностью данного курса является то, что выделены основные варианты использования Git'а. И показано как все эти варианты использования реализуются в основных инструментах (Shell, текстовый редактор VSCode, IDE PHPStorm и GUI для Git'а Sourcetree)

## Настройка различных инструментов для работы с Git

- Shell: Cmder: PowerShell: Posh-Git: Installation: запустить PowerShell с правами администратора и выполнить: "Install-Module posh-git"
- VSCode:
  - [Cmder & VS Code Integration](https://github.com/cmderdev/cmder/wiki/Seamless-VS-Code-Integration)
  - Git extensions for VSCode:
    - `Git Extension Pack` by Don Jayamanne:
      - Cons: Miss [`gitflow`](https://marketplace.visualstudio.com/items?itemName=vector-of-bool.gitflow), `Git Merger`
- PHPStorm: Settings | Tools | Terminal | `"cmd.exe" /k "<path_to_cmder>\vendor\init.bat"`
- GitLab, SourceTree - ничего настраивать не нужно

## Основные варианты использования

### Инициализация Git репозитория

- Shell: `git init`
- VSCode: `Git: Initialize Repository`
- PHPStorm: VCS | Import into Version Control | Create Git Repository...
- Sourcetree: New tab | Create

### Игнорирование файлов `.gitignore`

- VSCode: [`gitignore` extension](https://github.com/CodeZombieCH/vscode-gitignore) - A simple extension for Visual Studio Code that lets you pull .gitignore files from the [repository](https://github.com/github/gitignore):
  - добавляется команда `Add gitignore` с поддержкой шаблонов - как в плагине ".ignore" в PHPStorm
  - Cons:
    - При добавлении какого-либо шаблона в `.gitignore` несколько раз он добавляет несколько копий, хотя дублировать не нужно - в отличие от PyCharm
    - Этот extension позволяет добавлять в `.gitignore` только файлы, но не позволяет добавлять в `.gitignore` директории - в отличие от `.ignore` плагина для PHPStorm
  - Pros: included in the `Git Extension Pack`, [.NET Core Extension Pack]
- PHPStorm: плагин [.ignore](https://github.com/hsz/idea-gitignore) :
  - Pros: подчеркивает entries defined more than one - в отличие от `gitignore` extension в VSCode
- Sourcetree:
  - In Sourcetree you should be able to right click on one of the files/folders and select `ignore`. This will auto create a `.gitignore` file for you with that particular file/folder in it
  - Options | Git | Global Ignore List
  - Cons: нет шаблонов - в отличие от `gitignore` extension в VSCode, ".ignore" plugin in PHPStorm

### Работа с ветками

#### Что такое ветка в Git

Ветка в Git - это метка для коммита. The label moves to new commits as they are created. Когда вы содаете нову ветку вы ничего не изменяете в структуре репозитория. Вы просто создаете новую метку

В Git есть два типа веток:

- Локальные ветки - хранятся в директории .git/refs/heads/
- Удаленные (Remote-tracking) ветки

#### View branch list. List of branches

- Shell:
  - Local branches: `git branch`
  - Remote branches: `git branch -r`
- VSCode: кликнуть на текущем бранче в левом нижнем углу. Появится меню со списком бранчей
- PHPStorm: кликнуть на текущем бранче в правом нижнем углу. Появится меню со списком бранчей
- Sourcetree: список бранчей отобажается в левом sidebar'е в узле "BRANCHES"

#### Создание новой ветки

- Shell: `git branch <branch_name>`
- VSCode:
  - кликнуть на текущем бранче в левом нижнем углу. Появится меню с пунктами `Create new branch...` и `Create new branch from...`. При выборе пункта `Create new branch...` после создания бранча происходит checkout в этот бранч
  - `Git: Create Branch From...`, `Git: Create Branch`
  - [`Git Lens`](https://github.com/eamodio/vscode-gitlens): Branch Context menu | `Create Branch (via Terminal)...`
- PHPStorm: кликнуть на текущем бранче в правом нижнем углу. Появится меню с пунктом "New Branch"
- Sourcetree: Repository | Branch | New Branch

#### Узнать какая текущая ветка

- Shell:
  - В Cmder & Posh-Git текущий бранч отображается в приглашении консоли. Но следует помнить, что это значение не изменяется при изменении текущего бранча иными способами
  - `git status`
- VSCode: текущий бранч отображается в левом нижнем углу
- PHPStorm: текущий бранч отображается в правом нижнем углу
- Sourcetree: текущий бранч выделен жирным шрифтом

#### Checkout branch

##### Checkout branch during create

- Shell: `git checkout -b feature` # Создаёт новую ветвь, названную "feature" и делает её активной
- VSCode:
  - `Git: Create Branch`: после создания бранча происходит checkout в этот бранч
  - кликнуть на текущем бранче в левом нижнем углу. Появится меню с пунктами `Create new branch...` и `Create new branch from...`. При выборе пункта `Create new branch...` после создания бранча происходит checkout в этот бранч
- PHPStorm: кликнуть на текущем бранче в правом нижнем углу. Появится меню с пунктом "New Branch". В окне "Create New Branch" есть галка "Checkout branch"
- Sourcetree: Repository | Branch | New Branch. Есть галка "Checkout New Branch"

##### Checkout branch after create

- Shell: `git checkout <branch_name>`
- VS Code:
  - Можно кликнуть на названии бранча в левом нижнем углу и выбрать из меню новый бранч
  - `Git: Checkout to...` command
  - [Git Lens`](https://github.com/eamodio/vscode-gitlens):
    - Branch Context menu | `Checkout`
    - справа от названия бранча есть конка "Checkout"
  - Cons: При переключении ветки в VS Code текущий бранч в Cmder не изменяется
- PHPStorm:
  - переключатель бранчей находится в правом нижнем углу, в status bar'е
  - Cons: При переключении ветки в VS Code текущий бранч в Cmder не изменяется
- SourceTree:
  - двойной клик на бранче
  - Main menu | Repository | Checkout...
  - SourceTree при переключении бранчей переключает их со всеми изменениями, не перенося изменения в stash

#### Удалить локальную ветку

- Shell:
  - `git branch -d <branch_name>`
  - `git branch -D <branch_name>`
- VS Code:
  - `Git: Delete Branch...`. Эта команда удаляет только локальные бранчи. Удалить с помощью этой команды remote branch нельзя
  - [`Git Lens`](https://github.com/eamodio/vscode-gitlens): Branch Context menu | `Delete Branch (via Terminal)`. Этот способ для remote branches не работает
- PHPStorm: кликнуть на текущем бранче в правом нижнем углу. Появится меню со списком бранчей. Кликнуть на стрелочку справа от бранча. В открывшемся меню выбрать "Delete"
- Sourcetree:
  - from context menu: "Delete <branch_name>..."
  - Main menu | Repository | Branch | Delete Branches
  - при выполнении "Git-flow | Finish Feature" в окне "Finish Feature" есть галки "Delete branch" и "Force deletion"

#### Переименовать ветку

- Shell: `git branch -m old_branch new_branch`
- VSCode: `Git: Rename Branch...` - переименовывает текущий бранч
- PHPStorm: кликнуть по стрелочке справа от имени branch'а и появится "Rename..."
- Sourcetree: Branch context menu: "Rename <branch_name>..."
- GitLab: [Cannot rename branches](https://gitlab.com/gitlab-org/gitlab-ce/issues/50840)

#### Сравнить две ветки

- Shell: `git diff branch1 branch2`
- VSCode:
  - Git Lens: `COMPARE` node
  - [`GitLab Workflow`](https://gitlab.com/fatihacet/gitlab-vscode-extension):
    - `GitLab: Compare current branch with master` - открывает сравнение бранчей в GitLab'е
- PHPStorm:
  - Git | Compare with branch - сравнивает один файл
  - Выбрать бранч (либо Context menu | Git | Repository | Branches | \<choose branch\>, либо кликнуть на текущем бранче в правом нижнем углу), кликнуть по стрелочке справа от бранча и выбрать "Compare with Current" - сравнивает все файлы в бранче
- Sourcetree: щелкнуть правой кнопкой мыши на ветке и выберать из контекстного меню пункт "Diff against current" (current refers to the branch you are currently working on). This will give you the diff between the head commits of the two branches

#### Работа с удаленными (Remote-tracking) ветками

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
  - Pros: Sourcetree позволяет пушить сразу несколько веток - в отличие от PHPStrom

#### Слияние

- Shell: `git merge`
- VS Code:
  - `Git: Merge Branch...`
  - `Git Merger` extension:
    - Cons: missed in the `Git Extension Pack`
- PHPStorm: кликнуть на текущем бранче в правом нижнем углу), кликнуть по стрелочке справа от бранча и выбрать `Merge into Current`
- Sourcetree: Branch context menu | Merge <branch_name> into current branch

##### Разрешение базовых клнфликтов слияния

- Shell:

    Merge conflicts occur when the same part of the code has been modified in both branches. For example, if the same line of README.md is edited in fix and master:

    ```shell
    $ git merge fix
    # conflict with README.md
    # merge failed
    ```

    The file impacted will have conflict-resolution markers (`<<<<<<<` and `>>>>>>>`) added to it by git, showing the conflicting lines (separated by `=======`). Opening `README.md` in a text editor:

    ```shell
    To contact us email:
    <<<<<<< HEAD
    hello@enki.com
    =======
    help@enki.com
    >>>>>>> fix
    ```

    You have to manually choose the option you want or combine them. Then run `git add` to mark the file as resolved. When you're done resolving conflicts finalize the merge with `git commit`.
- VSCode:
  - Нажать на кнопку "Source Control" слева
  - See MERGE CHANGES in sidebar.
  - Those files have merge conflicts.
- PHPStorm: "Resolve Conflicts"
- Sourcetree: Main menu | Actions | Resolve Conflicts

### Работа с коммитами

#### Создание коммита

- Shell: `git commit -m <commit_message>`
- VSCode:
  - `Git: Commit`, `Git: Commit All`
  - нажать на кнопку "Source Control". В открывшемся sidebar'е есть сверху кнопка "Commit"
- PHPStorm:
  - кнопка Commit на Toolbar'е
  - Main menu| VCS | Commit
- Sourcetree:
  - Нажать на кнопку "Commit" на панели инструментов
  - В окне "Unstaged files" содержатся все непроиндексированные изменения. Выберать файлы для индексации перед коммитом
  - В окне "Staged files" содержатся все проиндексированные файлы. Для удаления файла из индекса нажать на "минус" справа от файла
  - Ввести комментарий к коммиту
  - Нажать кнопку "Commit" для фиксации всех проиндексированных изменений в репозитории

#### Partial commits

- VS Code: `Git: Stage Selected Ranges`
- PHPStorm: в окне "Commit Changes" можно галочками выбирать изменения
- Sourcetree: WORKSPACE | File Status: you can select lines to stage in the diff view of each uncommitted file. Then you commit what is in staging

#### Cherry-pick

Cherry-picking is the method to apply a single, specific commit from another branch. This is most useful when you are unable to merge the two branches. For example, you might want to fix a security issue present in both branches.

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

#### Revert commit - This generates a new commit with all the changes introduced in \<commit\> afterwards applying it to the current branch

- Shell: `git revert <commit>`.
- VSCode: [`Git History`](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory):
  - Context menu | Git: View File History. В открывшемся окне "File History" справа от каждого коммита есть кнопка "Cherry pick, Compare, etc". В открывшемся меню есть пункт "Revert this (...) commit"
- PHPStorm:
  - VCS | Git | Revert...
  - кнопка "Revert" на Toolbar'е
- Sourcetree: Commit context menu | Reverse commit...
