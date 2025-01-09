# Ubuntu安装NVM

# macOS/Linux配置方法

虽然可以使用项目包管理工具安装NVM（比如：[Homebrew](https://brew.sh/)、[APT](https://en.wikipedia.org/wiki/APT_(software))），但还是**推荐macOS和Linux使用手动配置方法**（Git安装、常规安装），安装NVM，本文也是讲解使用非项目包管理器安装NVM。

## Opt2:Git安装

1. 官方也推荐使用Git进行配置，但是官方的还是使用Github。国内的连接…… 所以，我推荐使用Gitee，在Terminal上一次输入：

```bash
# 进入家目录
cd ~
# 下载源码
git clone https://gitee.com/mirrors/nvm.git
# 重命名为.nvm
mv nvm .nvm
```

> 我们安装好NVM以后，我们需要配置到环境变量



2. 现在使用`nvm --version`，如果提示`nvm command not found`还是有问题。

解决`nvm command not found`问题，进入`.nvm`文件夹，新建`.bash_profile`

```bash
touch .bash_profile //新建文件

vim .bash_profile //打开文件
```



3. 在环境变量内，追加以下内容：

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```



4. 然后关闭文件，执行文件。终端输入：`source .bash_profile`



5. 终端输入：`nvm --version`出现版本号表示安装成功，就不会报`command not find`了。




## 配置国内源

大陆这边连接Node和NPM源有点忙，进而NVM也比较慢，所以我们使用前换成国内源。
临时使用：在终端内输入

```bash
export NVM_NODEJS_ORG_MIRROR=https://npmmirror.com/mirrors/node/
```

需要长期使用，就配置到配置文件里。



##nvm常用命令

```bash
nvm v    查看nvm版本 

nvm current    查看当前使用的node版本

nvm install latest   下载最新的node版本

nvm install 9.7.1   安装9.7.1版本 ( 默认安装64位 )

nvm install 9.7.1 32    安装32位的9.7.1版本

nvm uninstall 9.7.1    卸载9.7.1版本

nvm use 9.7.1    切换node版本至9.7.1

nvm list    查看本地已安装的node版本，同时也会显示当前使用的node版本
```




## 参考链接

[Windows/macOS/Linux上安装Node.js，并使用NVM管理多版本Node.js - 雨月空间站 (mintimate.cn)](https://www.mintimate.cn/2021/07/26/nvmNode/#Opt2-Git%E5%AE%89%E8%A3%85)

[服务器Ubuntu安装nvm踩坑篇-CSDN博客](https://blog.csdn.net/handsomezhanghui/article/details/111872159)

