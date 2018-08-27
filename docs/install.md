## Linux

Ubuntu:

`sudo apt-get install git`

Centos:

`yum –y install git`

## macOS

文件安装：

从 [该地址](https://git-scm.com/download/mac) 下载安装。

Homebrew：

1. 安装 Homebrew, [Homebrew 中文文档](https://brew.sh/index_zh-cn)
2. `brew install git`

## Windows

[下载地址](https://git-scm.com/download/win),双击下载文件，下一步，下一步... 完成。

## 初次运行配置

### 配置文件

1. `/etc/gitconfig` 文件: 包含系统上每一个用户及他们仓库的通用配置。 如果使用带有 `--system` 选项的
`git config` 时，它会从此文件读写配置变量。
2. `~/.gitconfig` 或 `~/.config/git/config` 文件:只针对当前用户。 可以传递 `--global` 选项让 Git 读写此文件。
3. 当前使用仓库的 Git 目录中的 `config` 文件(就是 `.git/config` ):针对该仓库。

在 Windows 系统中，Git 会查找 `$HOME` 目录下(一般情况下是 C:\Users\$USER)的 `.gitconfig` 文件。 Git 同样也会寻找 `/etc/gitconfig` 文件，但只限于 MSys 的根目录下，即安装 Git 时所选的目标位置。

### 用户信息

每一个 Git 的提交都会使用这些信息，并且它会写入到你的每一次提交中，不可更改:

```
git config --global user.name "xxx"
git config --global user.email "xxx@xx.com"
```

当你想针对特定项目使用不同的用户名称与邮件地址时，可以在那个项目目录下运行没有 `--global` 选项的命令来配置。

每一个级别覆盖上一级别的配置，所以 `.git/config` 的配置变量会覆盖 `/etc/gitconfig` 中的配置变量。

### 检查配置

- `git config --list` 列出所有Git当时能找到的配置。
-  `git config <key>` 来检查 Git 的某一项配置。

### 生成、添加公钥

- 生成 sshkey: `ssh-keygen -t rsa -C "xxxxx@xxxxx.com"`
- 按照提示完成三次回车，即可生成 ssh key。
- 通过查看 `~/.ssh/id_rsa.pub`。

![](http://ww1.sinaimg.cn/large/006t9e3Igy1fuoo2d6nrlj31200lmajn.jpg)

- 将公钥复制并添加到您的服务商公钥管理处。