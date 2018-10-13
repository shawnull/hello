## 本地管理多个 SSH Key

如何同一个电脑上添加并使用多个 SSH Key？

1. 使用 `ssh-keygen` 命令生成多个 SSH Key。要注意每次为密钥提供不同文件名，以避免覆盖已经存在的密钥。

2. 创建 `~/.ssh/config` 配置多个 SSH Key 的使用情形，示例如下：

   ```
   # 主机名 example.com 将使用  ~/.ssh/id_rsa 为私钥
   Host example.com
   HostName example.com
   User git
   IdentityFile ~/.ssh/id_rsa
   
   # 主机名 one.example.com 将使用  ~/.ssh/id_rsa_2 为私钥
   Host one.example.com
   HostName example.com
   User git
   IdentityFile ~/.ssh/id_rsa_2
   
   # 其它为配置的主机名将使用默认的   ~/.ssh/id_rsa 为私钥
   ```

## 本地管理多个 Git 账户

Github 限制一个 SSH 公钥只能被一个账户使用。如果你有多个 Github 账户，并且还有一个公司的 Git 账户，就需要在本地生成并管理多个 SSH Key。

首先需要对本地 SSH 进行配置，示例如下：

```
# 配置 Github 账户中常用的一个作为默认 Github 账户 
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

# 配置另外一个 Github 账户
Host shawnull.github.com
HostName github.com
User git
IdentityFile ~/.ssh/shawnull_id_rsa

# 配置公司 Git 账户
Host git.company.com
HostName company.com
User git
IdentityFile ~/.ssh/company_id_rsa

# 其余主机将使用默认私钥 ~/.ssh/id_rsa
```

然后需要为本地 Git 仓库指定用户信息：

```
$ cd repo_dir
$ git config user.name shawnull
$ git config user.email shawnull@163.com
```

并为该仓库指定远程仓库的地址（假设是 Github 账户 shawnull  的远程仓库）：

```
$ git remote add origin git@shawnull.github.com:shawnull/hello.git
```

