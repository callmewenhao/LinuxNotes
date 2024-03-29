## 包管理

**常见Linux系统与其包管理工具**

<img src="images/包管理.png" height=200>

### Ubuntu

Ubuntu 16.04 之前的版本使用：apt-get 和 apt-cache

Ubuntu 16.04 以及之后的版本使用：**apt**， 比 apt-get 用起来更简单，用户体验更好

| apt 命令         | 取代的命令           | 命令的功能                     |
| ---------------- | -------------------- | ------------------------------ |
| **apt install**  | apt-get install      | 安装软件包                     |
| apt remove       | apt-get remove       | 移除软件包                     |
| apt purge        | apt-get purge        | 移除软件包及配置文件           |
| **apt update**   | apt-get update       | 刷新存储库索引                 |
| **apt upgrade**  | apt-get upgrade      | 升级所有可升级的软件包         |
| apt autoremove   | apt-get autoremove   | 自动删除不需要的包             |
| apt full-upgrade | apt-get dist-upgrade | 在升级软件包时自动处理依赖关系 |
| apt search       | apt-cache search     | 搜索应用程序                   |
| apt show         | apt-cache show       | 显示装细节                     |

系统依赖安装：

```shell
以安装zip为例
$ apt update    # 只需要执行一次，不用每次都执行
$ apt install -y zip

如果不知道包名
$ apt update    # 只需要执行一次，不用每次都执行
$ apt search xxxxx
```

