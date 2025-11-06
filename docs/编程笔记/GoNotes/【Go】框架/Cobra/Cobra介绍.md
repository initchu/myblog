# Cobra 介绍

# 简要
Cobra <font style="color:rgb(51, 51, 51);">是一个 cli 接口模式的应用程序框架，同时也是生成该框架的命令行工具。用户可以通过 </font>help <font style="color:rgb(51, 51, 51);">方式快速查看该二进制的使用方式。</font>

Cobra <font style="color:rgb(51, 51, 51);">主要包括以下部分：</font>

+ Command<font style="color:rgb(51, 51, 51);">：一般表示 action，即运行的二进制命令服务。同时可以拥有子命令（children commands）。</font>
+ Args<font style="color:rgb(51, 51, 51);">：命令执行相关参数。</font>
+ Flags：<font style="color:rgb(51, 51, 51);">二进制命令的配置参数，可对应配置文件。参数可分为全局参数和子命令参数。参考：</font>[pflag library](https://github.com/spf13/pflag)<font style="color:rgb(51, 51, 51);">。</font>

# <font style="color:rgb(51, 51, 51);">安装</font>
<font style="color:rgb(51, 51, 51);">通过以下操作可以在 </font>$GOPATH/bin <font style="color:rgb(51, 51, 51);">安装 cobra 的二进制命令。</font>

```go
go get -u github.com/spf13/cobra/cobra
```

# <font style="color:rgb(51, 51, 51);">使用</font>
```powershell
# cobra
Cobra is a CLI library for Go that empowers applications.
This application is a tool to generate the needed files
to quickly create a Cobra application.

Usage:
  cobra [command]

Available Commands:
  add         Add a command to a Cobra Application
  help        Help about any command
  init        Initialize a Cobra Application

Flags:
  -a, --author string    author name for copyright attribution (default "YOUR NAME")
      --config string    config file (default is $HOME/.cobra.yaml)
  -h, --help             help for cobra
  -l, --license string   name of license for the project
      --viper            use Viper for configuration (default true)

Use "cobra [command] --help" for more information about a command.
```



> 更新: 2022-08-03 12:57:46  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/lfsyeo>