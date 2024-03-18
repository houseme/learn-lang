# Rust 入门篇：从 Hello World 开始掌握系统语言

---

对于计算机程序员来说，学习一门新的编程语言总是令人兴奋的。今天，我们就一起开始学习 Rust 语言的基础知识。作为一种现代的系统编程语言，Rust
提供了卓越的性能、内存安全和数据并发处理能力，同时避免了诸如空指针、数据竞争等历史遗留问题。让我们从一个简单的 Hello World
程序开始，循序渐进地探索 Rust 的奥秘。

## 安装 Rust 环境

在开始编写 Rust 代码之前，我们首先需要在系统中配置 Rust
环境。访问[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install),根据您的操作系统选择合适的安装方式。

对于基于 Unix 的系统 (Linux、macOS),您可以运行以下命令进行安装：

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

而在 Windows 系统上，可以下载 Rust 安装程序进行傻瓜式安装。

安装完成后，您可以在终端中输入`rustc --version`命令来验证 Rust 编译器是否已正确安装。

## Hello World

Rust 环境就绪后，我们就可以创建第一个 Rust 程序了。使用您喜欢的文本编辑器，新建一个文件`main.rs`,并输入以下内容：

```rust
fn main() {
    println!("Hello, World!");
}
```

这个简单的程序只包含一行代码，它调用了 Rust 标准库中的`println!`宏，用于在终端中打印"Hello, World!"。

在终端中，导航到包含`main.rs`文件的目录。然后输入以下命令编译并运行程序：

```
rustc main.rs
./main
```

您应该会在终端上看到"Hello, World!"被打印出来。祝贺您已经成功运行了第一个 Rust 程序！

## Cargo 构建工具

虽然我们可以手动编译和执行 Rust 程序，但 Rust 提供了一个强大的包管理和构建工具 Cargo，它可以极大地简化这一过程。

首先，通过运行`cargo new hello_world`来创建一个新的 Cargo 项目。这将创建一个`hello_world`目录，其中包含管理 Rust 项目所需的文件。

接下来，使用文本编辑器打开`hello_world/src/main.rs`文件，将之前的`println!`代码复制进去。

现在，您可以通过以下命令来构建和运行项目：

```
cargo build     # 编译项目
cargo run       # 运行项目
```

Cargo 会自动获取项目所需的依赖库，并对源代码进行编译和链接。当您修改代码时，只需再次运行`cargo build`或`cargo run`,Cargo
就会重新构建项目。

## 所有权和借用

所有权 (Ownership) 是 Rust 语言最与众不同的特性之一。Rust 为每个值都指定了一个变量作为其所有者。只有拥有值的所有权，才能使用该值。这种机制保证了内存安全，并消除了数据竞争等常见问题。

例如，当您创建一个字符串时，它是有一个所有者的：

```rust
let s = String::from("hello");  // s 是字符串的所有者
```

您可以将所有权转移给另一个变量：

```rust
let x = s;  // x 现在是字符串的所有者，s 不再有效
```

如果只需要临时访问值而不获取所有权，可以使用借用 (Borrowing)。借用会创建一个引用，指向值的所有者。与引用相关的概念还有作用域和生命周期，这些将在后续的学习中详细介绍。

```rust
let x = String::from("hello");
let y = & x; // y 是 x 的引用，x 仍然是字符串的所有者
```

## 结构化数据

在 Rust 中，您可以使用各种原生类型来表示结构化数据，如元组、数组和结构体。

**元组**是一种将多个其他值的组合成单个复合值的方式。例如：

```rust
let tuple = (1, 3.14, true);
```

**数组**是相同类型元素的集合，其长度是固定的。例如：

```rust
let array = [1, 2, 3, 4, 5];
```

**结构体**是您可以定义的自定义数据类型，用于打包不同类型的数据。例如：

```rust
struct Person {
    name: String,
    age: u32,
}

let p = Person {
name: String::from("Alice"),
age: 30,
};
```

## 函数和模块

函数和模块是 Rust 中组织和重用代码的两个核心概念。

**函数**使用`fn`关键字进行定义，可以接收参数并返回值。例如：

```rust
fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

**模块**则允许您将代码分组为单独的逻辑单元。使用`mod`关键字定义模块，使用`use`语句将模块引入作用域。例如：

```rust
mod math {
    fn add(a: i32, b: i32) -> i32 {
        a + b
    }
}

use math::add;

fn main() {
    println!("{}", add(2, 3)); // 输出 5
}
```

通过组合使用函数和模块，您可以编写出结构良好、可维护性强的 Rust 程序。

以上就是 Rust 语言入门的基本知识。在接下来的学习中，我们将继续探讨更多高级主题，如错误处理、并发编程、泛型和特征等。Rust
之路任重而道远，但只要持之以恒，定能编写出安全高效的系统级程序。让我们继续努力，共同开启 Rust 编程之旅！