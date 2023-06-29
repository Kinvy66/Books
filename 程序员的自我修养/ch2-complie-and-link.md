# 第2章 编译和链接

### 1. 被隐藏了的过程

{% code title="hellol.c" lineNumbers="true" %}
```c
#include <stdio.h>

int main()
{
    printf("Hello World\n");
    return 0;
}
```
{% endcode %}

最基础的 `hello world` 在Linux系统下，我们通常使用gcc编译

{% code lineNumbers="true" %}
```bash
$gcc hello.c 
$ ./a.out
$ Hello World
```
{% endcode %}

上面的编译命令实际包含 <mark style="color:red;">**预处理**</mark> 、<mark style="color:red;">**编译**</mark>、<mark style="color:red;">**汇编**</mark>和<mark style="color:red;">**链接**</mark>** 。**

我们可以使用不同的参数将这些过程分开执行

#### **1.1 预编译**

使用`-E` 参数表示只进行预编译处理

{% code lineNumbers="true" %}
```bash
$ gcc -E hello.c -o hello.i
```
{% endcode %}

预编译过程主要处理源代码文件中的以 `#` 开始的预编译指令。比如 `#include` 、`#define` 等。



#### 1.2 编译

使用 `-S` 进行编译预处理过的`.i` 文件，生成汇编文件

```bash
$gcc -S hello.i -o hello.s
```

或者直接使`.c` 文件编译成汇编文件，即完成预处理和编译两个过程

```bash
$gcc -S hello.c -o hello.s
```

#### 1.3 汇编

使用汇编器生成目标文件

```bash
$ as hello.s -o hello.o
```

或者：

```bash
$ gcc -c hello.s -o hello.o
```

#### 1.4 链接

使用 `ld` 工具链接

```bash
ld hello.o  #其他.o 文件
```

