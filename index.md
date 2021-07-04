# 中文Git与GitHub简单入门指南
注：
1. 本文Git概念的翻译均参照[码云 Gitee](https://gitee.com/)，未找到翻译的概念直接使用英文。
1. 命令代码中尖括号（“<……>”）中的内容是此处应输入的内容的描述，在使用时，尖括号含其中的描述内容应被替换为相应的内容。

## Git与GitHub简介
### Git是什么？
Git是一个免费开源的分布式版本控制系统。  
引用[Git官网](https://git-scm.com/)：
> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

功能：高效管理文件（尤其是代码）的历史变更、适合团队合作多人同时开发

官网：https://git-scm.com/

作者：Linus Torvalds，Linux系统的创造者

### GitHub是什么？  
GitHub是现在最流行的Git远程端托管服务提供商（下文简称托管商），现已被微软收购。GitHub也同时也因此成为了最大的开源软件托管网站。这些提供商一般也同时提供DevOps相关的功能。

其他类似的服务有：[GitLab](https://gitlab.com/)、[BitBucket](https://bitbucket.org/)、[码云 Gitee](https://gitee.com/)

### 入门资料
GitHub提供的一些Git入门文档：[GitHub Guides](https://guides.github.com/)  
其中包含一个可以动手操作的入门向导：[Hello World · GitHub Guides](https://guides.github.com/activities/hello-world/)

Atlassian的Git入门向导：[Learn Git- Git tutorials, workflows and commands | Atlassian Git Tutorial](https://www.atlassian.com/git)

Atlassian提供的相关Coursera课程：[Version Control with Git | Coursera](https://www.coursera.org/learn/version-control-with-git)

菜鸟教程：[Git 教程 | 菜鸟教程](https://www.runoob.com/git/git-tutorial.html)

### 概念翻译与简单解释
1. 仓库（repository）：被Git视作的一个独立的项目整体的一个文件夹，也简称repo
1. 提交（commit）：作名词表示仓库内容的一个历史节点，作动词表示创建一个新的提交
1. 工作区（working tree）：仓库文件夹下的目录结构（除.git文件夹外）
1. 暂存区（staging area）：工作区中即将被加进下一个提交的文件
1. untracked/unstaged、staged、tracked：不在暂存区中的文件的状态叫做untracked/unstaged，暂存区中文件的状态叫做staged，staged的文件和在commit中的文件统称tracked
1. 分支（branch）：提交历史的一个发展方向
1. HEAD：当前操作的一个分支中的一个提交

## 命令与操作：个人使用或小型非专业团队协作
### 中心化工作流与线性图模型
Git提交的线性图模型：每一个提交至多有一个父节点和一个子节点，形成一条链，代表项目的历史发展。

中心化工作流：所有的提交都在主分支（master）上进行。

![](https://www.atlassian.com/dam/jcr:f03a0fbd-a880-477f-aa32-33340383ce07/02%20(3).svg)

### 仓库初始化
#### git-init
git-init用于初始化一个Git仓库。

在命令行下进入一个文件夹，输入以下命令即可创建一个本地Git仓库：
```
git init
```

### 工作与记录历史
#### git-add
git-add用于将文件加入暂存区。

输入以下命令将一个文件加入暂存区：
```
git add <文件名>
```

输入以下命令将当前目录下的所有文件加入暂存区：
```
git add .
```

##### .gitignore
一个.gitignore文件用于指明所在目下Git忽略的untracked的文件（tracked的文件不影响）。

#### git-commit
git-commit用于提交暂存区中的文件。

输入以下命令提交并启动一个文本编辑器输入提交信息：
```
git commit
```

输入以下命令将提交信息作为命令参数提交：
```
git commit -m "<提交信息>"
```



#### git-stash
git-stash用于把暂存区中相比于上一个commit改变过的内容清楚并暂时存到stash中，stashed的内容不会与远程仓库同步。

输入以下命令stash：
```
git stash
```

输入以下命令恢复stash的内容：
```
git stash pop
```

stash可以跨多个提交进行。

### 查询信息
### git-status
git-status用于显示Git仓库的当前状态信息，包括文件信息等。

输入以下命令显示Git仓库的当前状态信息：
```
git status
```

### git-log
git-log用于显示提交历史。

输入以下命令显示详细的提交历史：
```
git log
```

一些可选参数：
1. `--oneline`：每个提交只显示一行
1. `--graph`：以图的形式显示
1. `--all`：显示所有

以下命令最常用于大致查看提交历史的图结构：
```
git log --oneline --graph --all
```

### git-checkout
git-checkout用于将工作区的文件和HEAD转换到某一个分支或者提交，会将工作区的所有文件替换为对应分支或者对应提交的文件。

输入以下命令checkout：
```
git checkout <分支名字或提交ID>
```

### 修复与重构
***警告：此部分的操作会修改Git提交历史的结构，若你要修复或重构的提交已被同步到远程端并与他人分享，请尽量避免这些操作。***

#### 修复提交（`commit --amend`）
在git-commit命令中加入`--amend`参数用于修复（覆盖）上一个提交，而不是创建一个新的提交。

输入以下命令进行修复提交：
```
git commit --amend
```
```
git commit --amend -m "<新的提交信息>"
```

#### `reset HEAD~`
`reset HEAD~`用于撤销上一个commit操作。

具体操作请参考：[version control - How do I undo the most recent local commits in Git? - Stack Overflow](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)

### 远程仓库与同步
#### 在GitHub上创建远程仓库
在自己的主页点击“New”创建新仓库，或直接访问页面[Create a New Repository](https://github.com/new)。

按照惯例，Git仓库命名为全小写，中间用连字符“-”连接。

如果你在GitHub上创建仓库，并选择了以下任意一个或多个文件，会自动第一次提交并包含这些文件：
1. README.md：Markdown格式的项目与仓库说明
1. LICENSE：开源协议
1. .gitignore：如上

#### 远程仓库与追踪分支
一个本地Git仓库可以设置其对应的远程Git仓库，一个远程仓库的信息包含其名字和URL。默认的远程仓库名字为“origin”。

一个分支可以对应远程仓库的一个分支，称为远程分支；本地分支有对应的远程分支后，会自动创建一个分支记录这一远程分支，叫做追踪分支，以`<远程仓库名或URL>/<分支名>`表示，如`origin/master`。

##### git-remote
git-remote用于管理远程仓库的名字与URL。

输入以下命令为本地仓库添加名为origin的远程仓库：
```
git remote add origin <远程仓库URL>
```

输入以下命令显示远程仓库设置：
```
git remote -v
```

#### git-clone
git-clone用于将一个远程仓库克隆到本地。

输入以下命令克隆一个远程仓库：
```
git clone <远程仓库URL>
```

#### git-fetch
git-fetch用于下载远程分支更新追踪分支。

输入以下命令fetch：
```
git fetch
```

#### git-pull
git-pull相当于先fetch后再将追踪分支合并到本地分支。若远程分支和本地分支没有冲突，它相当于下载远程分支直接更新本地分支。

输入以下命令pull：
```
git pull
```

注：对于个人单分支项目，一般直接pull即可；对于多分支项目，为避免不必要的合并，应先fetch后检查冲突，若有冲突，决定选择合并或是rebase本地冲突的提交。

#### git-push
git-push用于上传本地分支更新远程分支。

输入以下命令push：
```
git push
```

在一个本地分支第一次push时，需要在push时设置远程分支：
```
git push -u `<远程仓库名或URL>/<分支名>`
```

在远程分支与本地分支冲突时，可以输入以下命令强行push覆盖远程分支（***警告：此操作会删除远程分支中冲突的提交，且无法恢复，某一些被保护的远程分支不允许强行push***）：
```
git push --force
```
注：在修复与重构后且确定修改无误后，你需要使用强行push更新远程分支。

### 小型非专业团队协作建议
团队要求：
1. 一般来说3人以内（GitHub免费私有仓库的成员人数也最多为3人）；
1. 工作时，团队任意两人可以随时联系到对方；

协作规范（防止在旧版代码上修改）：
1. 每次开始工作之前先pull；
1. 每个人push后通知其他所有人pull；
1. 在commit之前pull。

## 大型或专业团队协作
注：若你需要在一个大型或专业团队中管理一个企业级项目或开源项目的开发，则应该系统地完整地学习Git，因此下文不提供详细教程，只提供一些需要学习内容的简要说明和参考链接。

Git提交的图模型：一个Git仓库的所有提交构成一个DAG（有向无环图）。  
使用命令行查看复杂的提交图效果一般，可以使用Atlassian的[Sourcetree](https://www.sourcetreeapp.com/)软件方便直观地查看提交图。

工作流：[Git Workflow | Atlassian Git Tutorial](https://www.atlassian.com/git/tutorials/comparing-workflows)

### 初始化
#### Fork
Fork不是Git本身提供的功能，而是很多Git托管商提供的功能，用于将他人账户下的Git仓库复制到自己仓库下。

### 工作与记录历史
#### git-branch
git-branch用于管理Git仓库的分支。

#### git-merge
git-merge用于合并Git仓库的分支。

#### Pull request
Pull request不是Git本身提供的功能，而是很多Git托管商提供的功能，用于提出让他人对自己的代码给出建议的请求、或者将自己的分支合并到自己没有权限操作的分支的请求，同时可用于代码评审。

### 修复与重构
***警告：此部分的操作会修改Git提交历史的结构，若你要修复或重构的提交已被同步到远程端并与他人分享，请尽量避免这些操作。***

### git-rebase与交互性rebase
rebase相关功能用于重构Git提交图的结构。

### 大型或专业团队协作
团队要求：
1. 有一个或多个仓库维护者，应能熟练使用Git的各项功能；
1. 其他人应了解“个人使用或小型非专业团队协作”中的内容并听从维护者指导。

协作规范：
1. 明确主要分支和团队每个人的操作权限（可能有多级）；
1. 仓库维护者负责审核自己负责的主要分支的pull request和将其他分支合并到此分支；
1. 所有人（包括维护者）不应该在主要分支直接提交，所有人在开发自己负责的部分时都应有自己的分支或者fork仓库（对于开源软件），在自己负责的模块在开发完成后，创建pull request请求维护者合并，此类合并不应该使用fast forward合并；
1. 不允许修改主要分支的历史，因此主要分支的每次合并都应仔细检查。

## 参考与推荐资料、课程、软件
1. Git官网：[Git](https://git-scm.com/)
1. Atlassian提供的相关Coursera课程：[Version Control with Git | Coursera](https://www.coursera.org/learn/version-control-with-git)
1. Atlassian的可视化版本控制软件：[Sourcetree | Free Git GUI for Mac and Windows](https://www.sourcetreeapp.com/)
1. VSCode的版本控制功能支持：[Version Control in Visual Studio Code](https://code.visualstudio.com/docs/editor/versioncontrol)
1. JetBrains软件的Git支持（以IntelliJ IDEA为例，其余软件类似）：[Git - Help | IntelliJ IDEA](https://www.jetbrains.com/help/idea/using-git-integration.html)
