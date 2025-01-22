### 生成ssh key

生成第一个ssh key：

```bash
cd ~/.ssh
ssh-keygen -t rsa -C "dreisteine262@163.com"
```

在 "Enter a file in which to save the key (/Users/you/.ssh/id_rsa):" 后输入账户名，如 "dreisteine262"，然后一路回车即可。

生成第二个ssh key：

```bash
ssh-keygen -t rsa -C "dreisteine262@outlook.com"
```

在 "Enter a file in which to save the key (/Users/you/.ssh/id_rsa):" 后输入账户名，如 "dreisteine_work"，然后一路回车即可。

### 设置公钥

接下来，在Github网页上设置两个账号的ssh key，分别为 "dreisteine262" 和 "dreisteine_work"。

### 添加私钥

```bash
eval $(ssh-agent -s)

ssh-add ~/.ssh/dreisteine262
ssh-add ~/.ssh/dreisteine_work
```

### 修改配置文件

```bash
touch ~/.ssh/config
```

在config文件中添加：

```bash
Host one
HostName ssh.github.com
IdentityFile ~/.ssh/dreisteine262

Host two
HostName ssh.github.com
IdentityFile ~/.ssh/dreisteine_work
```

### 测试

```bash
ssh –T git@one
ssh –T git@two
```

如果显示 "Hi dreisteine262! You've successfully authenticated, but GitHub does not provide shell access." 和 "Hi dreisteine_work! You've successfully authenticated, but GitHub does not provide shell access." 即成功。

### 继续设置

删除全局设置
```bash
git config --global --unset user.name
git config --global --unset user.email
```

在每个项目中单独添加本地设置，设置为私有仓库的GitHub账号邮箱和公有账号的GitHub邮箱。

```bash
git config --local user.name xxxx
git config --local user.email xxxx
```

之后在添加远程仓库的时候，把github.com修改成one或者two就好了（即上述文件中的HOST选项），用上面两个Host名称来代替原来的github.com ，（这一步很重要）如：

```bash
git remote add origin git@one:xxx/example.git # public user
git remote add origin git@two:xxx/example.git # priavate user
```