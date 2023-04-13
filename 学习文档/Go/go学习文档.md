安装外部库超时，执行以下命令

go env -w GOPROXY=https://goproxy.cn



go env -w GO111MODULE=  // auto on off

# 声明变量

```go
var a
a =1
// 或
var a = 1
// 或
var a int = 1
// 或
a := 1  // 不可在func 外使用这种声明方式，func 外必须以关键字开头，func var等
```

# 基础数据类型

 uint8类型，或者叫 byte 型，代表了ASCII码的一个字符。
 rune类型，代表一个 UTF-8字符。
 当需要处理中文、日文或者其他复合字符时，则需要用到rune类型。rune类型实际是一个int32。

 '' 代表字符 "" 代表string

 - 布尔型
 - 数字类型
 - 字符串类型
 - 派生类型
   - 指针
   - 数组
   - 结构体
   - 函数
   - 接口
   - map

```go
%v    值的默认格式表示。当输出结构体时，扩展标志（%+v）会添加字段名
%#v    值的Go语法表示
%T    值的类型的Go语法表示
%%    百分号
```

# go Mod 模式

`go mod init xxx`

>  go.mod文件一旦创建后，它的内容将会被go toolchain全面掌控。go toolchain会在各类命令执行时，比如go get、go build、go mod等修改和维护go.mod文件。

go.mod 提供了`module`, `require`、`replace`和`exclude` 四个命令

- `module`  语句指定包的名字（路径）
- `require` 语句指定的依赖项模块
- `replace` 语句可以替换依赖项模块
- `exclude` 语句可以忽略依赖项模块

# package

Go语言的包借助了目录树的组织形式，一般包的名称就是其源文件所在目录的名称，虽然Go语言没有强制要求包名必须和其所在的目录名同名，但还是建议包名和所在目录同名，这样结构更清晰。

包的习惯用法：

- 包名一般是小写的，使用一个简短且有意义的名称。
- 包名一般要和所在的目录同名，也可以不同，包名中不能包含`- `等特殊符号。
- 包一般使用域名作为目录名称，这样能保证包名的唯一性，比如 GitHub 项目的包一般会放到`GOPATH/src/github.com/userName/projectName `目录下。
- 包名为 main 的包为应用程序的入口包，编译不包含 main 包的源码文件时不会得到可执行文件。
- 一个文件夹下的所有源码文件只能属于同一个包，同样属于同一个包的源码文件不能放在多个文件夹下

## 包的引用格式

1. 标准引用格式`import "fmt"` fmt.xxx
2. 自定义别名引用格式 `import F "fmt"`F.xxx
3. 省略引用格式`import . "fmt"` xxx  这种方式相当于把代码合并过来
4. 匿名引用格式 `import _ "fmt"` 只执行init方法，不使用其中的方法

# 函数

```go
func 函数名(形式参数列表)(返回值列表){
  函数体
}
func demo(x,y int) int {
  return x + y
}
```

如果函数声明时，包含返回值列表，那么函数必须以return 语句结尾

- 可以在函数声明之前调用

# 数组

数组是值类型，传参，赋值都是值得拷贝

声明不定长数组 var a = [...]type，编译器推导长度

根据元素个数设置数组大小 var a = [...]type{x,x,x,x,x,x,x,....}

 多维数组**只有第一层**可以使用`...`来让编译器推导数组长度。 

> 1. 数组支持 “==“、”!=” 操作符，因为内存总是被初始化过的。
> 2. `[n]*T`表示指针数组，`*[n]T`表示数组指针 。



# 字符串

Go 语言中，字符串是只读的，也就意味着每次修改操作都会创建一个新的字符串。如果需要拼接多次，应使用 `strings.Builder`，最小化内存拷贝次数。

```go
var str strings.Builder
for i := 0; i < 1000; i++ {
    str.WriteString("a")
}
fmt.Println(str.String())
```

