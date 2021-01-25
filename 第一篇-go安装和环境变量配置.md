
### 安装go

一般我们安装go语言有下面三种方式

#### 使用 brew 安装

在终端输入`brew install go`或者`brew install golang`

#### 下载安装包 直接图形化界面安装

通过官网地址：[https://golang.org/dl/]( https://golang.org/dl/) 
下载mac安装包 点击安装即可


#### 使用 源码安装

当然我们也可以在官网： [https://golang.org/dl/]( https://golang.org/dl/) 
下载到源码 之后编译安装
```shell
tar -C /usr/local -xzf go1.15.6.linux-amd64.tar.gz
```

### 环境变量配置

无论使用哪种方式安装成功之后  我们都需要做环境变量的配置：

`GOROOT`：安装目录（go语言安装目录）

`GOPATH`：工程目录（自己工程项目目录）

`GOBIN`：可执行文件目录

`PATH`：将go可执行文件加入PATH中，使GO命令与我们编写的GO应用可以全局调用

其中`GOPATH`包含三个目录：`bin`、`pkg`、`src`

`src`目录：源文件。

`pkg`目录：编译好的库文件，主要是*.a文件。

`bin`目录：可执行文件。

需要将上面变量配置到` .bash_profile `（家目录下）中 然后使用`source .bash_profile`即时生效。

配置好之后可以使用`go env`查看 go语言的相关变量

我们可以使用 `go version` 查看安装的版本
```shell
# go version                                                                                                         ✔  11341  20:46:14
go version go1.15.5 darwin/amd64
```

 
至此我们的go语言学习环境就已经安装配置好了，开启新的语言学习了。💪