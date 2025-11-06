# 0 Hello Golang

## 你好，Golang！
```go
package main
import "fmt"
func main(){
    fmt.Println("Hello Golang!")
}
//单行注释

/*
这
是
多
行
注
释
 */
```

1. <font style="color:rgb(51, 51, 51);">第一行内容为“package main”，它表示这个源码文件属于main包。main包是每个Go应用程序都包含的包，有且只有一个。</font>
2. <font style="color:rgb(51, 51, 51);">第二行内容是“import “fmt"”，它的作用是导入名为“fmt”的包，目的在于稍后使用fmt包提供的各种能力。一旦某个包被导入，它必须被使用。</font>
3. <font style="color:rgb(51, 51, 51);">从第三行开始到最后，是main()函数，这个函数比较特殊，它是Go程序的“入口”函数，是程序运行的起点。这个函数必须存在且只能存在一个，且必须声明在main包中。任何一个Go函数都要求使用成对的大括号将函数体包裹起来。</font>
4. <font style="color:rgb(51, 51, 51);">第四行调用了fmt包中的Println()函数，这个函数的作用是将特定的内容输出到控制台上。</font>
5. <font style="color:rgb(51, 51, 51);">第五行是main()函数的结束。</font>

## SDK 命令行工具
### <font style="color:rgb(51, 51, 51);">go build</font>
<font style="color:rgb(51, 51, 51);">go build命令的作用是编译Go源码，并生成可执行的文件。</font>

<font style="color:rgb(51, 51, 51);">Go SDK 自 1.9 版本开始就支持并发编译了，能尽可能地发挥电脑的最大性能完成编译，所以 Go 源码的编译速度是非常快的。在编译过程中，除了我们自己写的代码外，如果使用了第三方的包，这些包会被一同编译。当我们执行go build命令后，会搜索当前目录下的go源码并完成编译。go build 命令还允许附加参数，方便开发者对编译参数进行配置，具体如下表所示：</font>

| <font style="color:rgb(51, 51, 51);">参数名</font> | <font style="color:rgb(51, 51, 51);">作用</font> |
| :---: | --- |
| <font style="color:rgb(51, 51, 51);">-v</font> | <font style="color:rgb(51, 51, 51);">编译时显示包名</font> |
| <font style="color:rgb(51, 51, 51);">-p x</font> | <font style="color:rgb(51, 51, 51);">指定编译时并发的数量（使用x表示），该值默认为CPU的逻辑核心数</font> |
| <font style="color:rgb(51, 51, 51);">-a</font> | <font style="color:rgb(51, 51, 51);">强制进行重新构建</font> |
| <font style="color:rgb(51, 51, 51);">-n</font> | <font style="color:rgb(51, 51, 51);">仅输出编译时执行的所有命令</font> |
| <font style="color:rgb(51, 51, 51);">-x</font> | <font style="color:rgb(51, 51, 51);">执行编译并输出编译时执行的所有命令</font> |
| <font style="color:rgb(51, 51, 51);">-race</font> | <font style="color:rgb(51, 51, 51);">开启竞态检测</font> |


<font style="color:rgb(51, 51, 51);">此外，如果我们希望只编译某个go源码文件或包，可在go build命令后添加文件或包名。例如，现有file1.go、file2.go和file3.go，我们只希望编译file1.go，便可如下执行：</font>

`go build file1.go`

### <font style="color:rgb(51, 51, 51);">go clean</font>
<font style="color:rgb(51, 51, 51);">go clean命令可以清理当前目录内的所有编译生成的文件，具体包括：</font>

+ <font style="color:rgb(51, 51, 51);">当前目录下生成的与包名或者 Go 源码文件同名的可执行文件，以及当前目录中_obj和_test目录中名为_testmain.go、test.out、build.out、a.out以及后缀为.5、.6、.8、.a、.o和.so的文件，这些文件通常是执行go build命令后生成的；</font>
+ <font style="color:rgb(51, 51, 51);">当前目录下生成的包名加“.test”后缀为名的文件，这些文件通常是执行go test命令后生成的；</font>
+ <font style="color:rgb(51, 51, 51);">工作区中pkg和bin目录的相应归档文件和可执行文件，这些文件通常是执行go install命令后生成的。</font>

<font style="color:rgb(51, 51, 51);">go clean命令还允许附加参数，具体参数和作用如下表所示：</font>

| <font style="color:rgb(51, 51, 51);">参数名</font> | <font style="color:rgb(51, 51, 51);">作用</font> |
| :---: | --- |
| <font style="color:rgb(51, 51, 51);">-i</font> | <font style="color:rgb(51, 51, 51);">清除关联的安装的包和可运行文件，这些文件通常是执行go install命令后生成的</font> |
| <font style="color:rgb(51, 51, 51);">-n</font> | <font style="color:rgb(51, 51, 51);">仅输出清理时执行的所有命令</font> |
| <font style="color:rgb(51, 51, 51);">-r</font> | <font style="color:rgb(51, 51, 51);">递归清除在 import 中引入的包</font> |
| <font style="color:rgb(51, 51, 51);">-x</font> | <font style="color:rgb(51, 51, 51);">执行清理并输出清理时执行的所有命令</font> |
| <font style="color:rgb(51, 51, 51);">-cache</font> | <font style="color:rgb(51, 51, 51);">清理缓存，这些缓存文件通常是执行go build命令后生成的</font> |
| <font style="color:rgb(51, 51, 51);">-testcache</font> | <font style="color:rgb(51, 51, 51);">清理测试结果</font> |


<font style="color:rgb(51, 51, 51);">在团队式开发中，通常在每次提交代码前执行go clean命令，防止提交编译时生成的文件。</font>

### <font style="color:rgb(51, 51, 51);">go run</font>
<font style="color:rgb(51, 51, 51);">go run命令的作用是直接运行go源码，不在当前目录下生成任何可执行的文件。</font>

<font style="color:rgb(51, 51, 51);">从原理上讲，go run只是将编译后生成的可执行文件放到临时目录中执行，工作目录仍然为当前目录。同时，go run命令允许添加参数，这些参数将作为go程序的可接受参数使用。</font>

<font style="color:rgb(51, 51, 51);">由此可见，go run命令同样会执行编译操作。但要注意的是，go run不适用于包的执行。</font>

### <font style="color:rgb(51, 51, 51);">gofmt</font>
<font style="color:rgb(51, 51, 51);">gofmt命令的作用是将代码按照Go语言官方提供的代码风格进行格式化操作。</font>

<font style="color:rgb(51, 51, 51);"></font><font style="color:rgb(51, 51, 51);">gofmt和go fmt是两个不同的命令</font><font style="color:rgb(51, 51, 51);">。go fmt命令是gofmt的封装，go fmt支持两个参数：-n和-x，分别表示仅输出格式化时执行的命令，以及执行格式化并输出格式化时执行的命令。</font>

<font style="color:rgb(51, 51, 51);">执行gofmt命令时，可指定文件或目录，也可不指定。当不指定时，gofmt命令会搜索当前目录中的go源码文件，并执行相应的格式化操作。</font>

<font style="color:rgb(51, 51, 51);">gofmt命令还允许附加参数，具体参数和作用如下表所示：</font>

| <font style="color:rgb(51, 51, 51);">参数名</font> | <font style="color:rgb(51, 51, 51);">作用</font> |
| --- | --- |
| <font style="color:rgb(51, 51, 51);">-l</font> | <font style="color:rgb(51, 51, 51);">仅输出需要进行代码格式化的源码文件的绝对路径</font> |
| <font style="color:rgb(51, 51, 51);">-w</font> | <font style="color:rgb(51, 51, 51);">进行代码格式化，并用改写后的源码覆盖原有源码</font> |
| <font style="color:rgb(51, 51, 51);">-r rule</font> | <font style="color:rgb(51, 51, 51);">添加自定义的代码格式化规则（使用rule表示），格式为：pattern -> replacement</font> |
| <font style="color:rgb(51, 51, 51);">-s</font> | <font style="color:rgb(51, 51, 51);">开启源码简化</font> |
| <font style="color:rgb(51, 51, 51);">-d</font> | <font style="color:rgb(51, 51, 51);">对比输出代码格式化前后的不同，依赖diff命令</font> |
| <font style="color:rgb(51, 51, 51);">-e</font> | <font style="color:rgb(51, 51, 51);">输出所有的语法错误，默认只会打印每行第1个错误，且最多打印10个错误</font> |
| <font style="color:rgb(51, 51, 51);">-comments</font> | <font style="color:rgb(51, 51, 51);">是否保留代码注释，默认值为true</font> |
| <font style="color:rgb(51, 51, 51);">-tabwidth x</font> | <font style="color:rgb(51, 51, 51);">用于指定代码缩进的空格数量（使用x表示），默认值为8，该参数仅在-tabs参数为false时生效</font> |
| <font style="color:rgb(51, 51, 51);">-tabs</font> | <font style="color:rgb(51, 51, 51);">用于指定代码缩进是否使用tab（“\t”），默认值为true</font> |
| <font style="color:rgb(51, 51, 51);">-cpuprofile filename</font> | <font style="color:rgb(51, 51, 51);">是否开启CPU用量分析，需要给定记录文件（使用filename表示），分析结果将保存在这个文件中</font> |


:::info
💡 提示：使用 -s 参数进行源码简化的规则请参考：

https://pkg.go.dev/cmd/gofmt#hdr-the_simplify_command

:::

### <font style="color:rgb(51, 51, 51);">go install</font>
<font style="color:rgb(51, 51, 51);">go install命令的作用和go build类似，都是将源码编译为可执行的文件，附加参数也基本通用，这里就不再赘述了。区别在于：</font>

+ <font style="color:rgb(51, 51, 51);">go install命令在编译源码后，会将可执行文件或库文件安装到约定的目录下；</font>
+ <font style="color:rgb(51, 51, 51);">go install命令生成的可执行文件使用包名来命名；</font>
+ <font style="color:rgb(51, 51, 51);">默认情况下，go install命令会将可执行文件安装到GOPATH\bin目录下，依赖的三方包会被安装到GOPATH\bin目录下。</font>

### <font style="color:rgb(51, 51, 51);">go get</font>
<font style="color:rgb(51, 51, 51);">go get命令的作用是获取源码包，这一操作包含两个步骤，分别是下载源码和执行go intall命令进行安装。使用时，仅需将源码仓库地址追加到go get后即可（访问</font>[pkg.go.dev/](https://link.juejin.cn/?target=https%3A%2F%2Fpkg.go.dev%2F)<font style="color:rgb(51, 51, 51);">，搜索包名，在包详情页可以找到仓库地址），例如：</font>

go get github.com/ethereum/go-ethereum 

<font style="color:rgb(51, 51, 51);">go get命令还允许附加参数，具体参数和作用如下表所示：</font>

| <font style="color:rgb(51, 51, 51);">参数名</font> | <font style="color:rgb(51, 51, 51);">作用</font> |
| --- | --- |
| <font style="color:rgb(51, 51, 51);">-d</font> | <font style="color:rgb(51, 51, 51);">仅下载源码包，不安装</font> |
| <font style="color:rgb(51, 51, 51);">-f</font> | <font style="color:rgb(51, 51, 51);">在执行-u参数操作时，不验证导入的每个包的获取状态</font> |
| <font style="color:rgb(51, 51, 51);">-fix</font> | <font style="color:rgb(51, 51, 51);">在下载源码包后先执行fix操作</font> |
| <font style="color:rgb(51, 51, 51);">-t</font> | <font style="color:rgb(51, 51, 51);">获取运行测试所需要的包</font> |
| <font style="color:rgb(51, 51, 51);">-u</font> | <font style="color:rgb(51, 51, 51);">更新源码包到最新版本</font> |
| <font style="color:rgb(51, 51, 51);">-u=patch</font> | <font style="color:rgb(51, 51, 51);">只小版本地更新源码包，如从1.1.0到1.1.16</font> |
| <font style="color:rgb(51, 51, 51);">-v</font> | <font style="color:rgb(51, 51, 51);">执行获取并显示实时日志</font> |
| <font style="color:rgb(51, 51, 51);">-insecure</font> | <font style="color:rgb(51, 51, 51);">允许通过未加密的HTTP方式获取</font> |


<font style="color:rgb(51, 51, 51);">若要指定所获取源码包的版本，可以通过添加“@版本号”的方式执行。如：</font>

go get github.com/ethereum/go-ethereum@v1.10.1 

<font style="color:rgb(51, 51, 51);">在使用Go SDK 1.17版本时，有一点需要额外注意：执行go get命令可能会收到警告，大意是go get命令是不建议使用的。此时，使用go install替换go get即可，原因是在未来的Go SDK版本中go get的作用等同于go get -d。</font>

<font style="color:rgb(51, 51, 51);">如果你对“go get”命令感兴趣，可以阅读官方对它的说明：</font>[docs.studygolang.com/doc/go-get-…](https://link.juejin.cn/?target=https%3A%2F%2Fdocs.studygolang.com%2Fdoc%2Fgo-get-install-deprecation)



> 更新: 2022-04-13 18:30:47  
> 原文: <https://www.yuque.com/xiaoshan_wgo/codingnotes/zl31hr>