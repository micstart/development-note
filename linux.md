
1. 设置环境变量  
- 查看环境变量：  
  `echo $PATH`
- 仅当前会话生效：  
  `PATH=$PATH:/usr/local/  
  export PATH="$PATH:/usr/local/bin"`
- 仅当前用户生效（或~/.bash_profile）：  
    sudo gedit ~/.bashrc
    export PATH=$PATH:/usr/local/bin
    source ~/.bashrc
- 所有用户生效：  
    sudo gedit /etc/profile
    export PATH=$PATH:/usr/local/bin
    source /etc/profile
参考：https://linux.cn/article-5478-1.html
