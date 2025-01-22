本文尝试在GitHub和BitBucket上配置多个SSH Keys，以便对不同类型（如基础研究、工程应用等）项目代码进行归纳管理，步骤如下：

- 查看已设置选项，并清除全局设置：
  
  ```bash
  git config --list
  ```
  
  ```bash
  git config --global --unset user.name "用户名"
  git config --global --unset user.email "邮箱"
  ```

- 使用邮箱分别生成对应GitHub和BitBucket的SSH Keys：
  
  ```bash
  ssh-keygen -t rsa -C "dreisteine262@163.com" -f ~/.ssh/github
  ssh-keygen -t rsa -C "dreisteine262@163.com" -f ~/.ssh/bitbucket_research
  ssh-keygen -t rsa -C "dreisteine262@163.com" -f ~/.ssh/bitbucket_project
  ```

- 添加公钥（即pub）：
  
  此步介绍略，请自行查看其它材料。

- 添加私钥（即identify）
  
  ```bash
  eval "$(ssh-agent -s)"
  ```
  
  ```bash
  ssh-add ~/.ssh/github
  ssh-add ~/.ssh/bitbucket_research
  ssh-add ~/.ssh/bitbucket_project
  ```

- 设置config文件：
  
  ```textile
  Host github.com
      HostName github.com
      IdentityFile ~/.ssh/github
      PreferredAuthentications publickey
      IdentitiesOnly yes
      IdentityAgent none
  
  Host bitbucket_research.org
      HostName bitbucket.org
      IdentityFile ~/.ssh/bitbucket_research
      PreferredAuthentications publickey
      IdentitiesOnly yes
      IdentityAgent none
  
  Host bitbucket_project.org
      HostName bitbucket.org
      IdentityFile ~/.ssh/bitbucket_project
      PreferredAuthentications publickey
      IdentitiesOnly yes
      IdentityAgent noneid_rsa
  ```
  
  测试连接：
  
  ```git
  ssh -T git@github.com
  ssh -T git@bitbucket_research.org
  ssh -T git@bitbucket_project.org
  ```

- 项目克隆：如果连接测试通过但是无法clone项目，则重新执行上述第4步；在clone项目的时候，选择ssh拉取，把**冒号前的域名**改成**Config中Host后跟随的名字**，比如：
  
  ```git
  git@bitbucket.org:aaa/xxx.git
  ```
  
  改成
  
  ```bash
  git@bitbucket_research.org:aaa/xxx.git
  ```

- 全局设置用户名和邮箱：
  
  ```bash
  git config --global --unset user.name "用户名"
  git config --global --unset user.email "邮箱"
  ```

- 最后，测试GitHub和GitBucket的Clone和Push功能是否正常，如：
  
  ```bash
  git clone git@github.com:Ulti-Dreisteine/gaussian-process-regression.git
  git clone git@bitbucket_project.org:project/cstr-mpc.git
  git clone git@bitbucket_research.org:dreisteine-research/adapt-control-tutorial.git
  ```
