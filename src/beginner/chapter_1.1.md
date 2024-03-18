# Rust 语言入门：从零开始掌握这门系统编程语言

## 安装 Rust 环境

在开始学习 Rust 之前，我们需要先为自己的系统设置好 Rust 开发环境。这一过程非常简单，只需要使用 Rust 官方提供的工具`rustup`
即可。

### Rustup 安装工具

`rustup`是 Rust 官方提供的工具链安装器，它可以帮助我们在不同平台上安装 Rust 工具链。

#### Windows 用户

对于 Windows 用户，可以在命令提示符中运行以下命令来安装`rustup`：

```
winget install Rustlang.Rustup
```

#### Linux 和 macOS 用户

对于 Linux 和 macOS 用户，可以在终端中运行以下命令来安装`rustup`：

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

安装过程中，可以一路选择默认选项即可。

### Rust 工具链

安装完`rustup`后，它会自动为我们安装 Rust 工具链，包括编译器`rustc`、构建工具`cargo`以及其他一些工具。

要检查工具链是否安装成功，可以在命令行中运行：

```bash
rustc --version
cargo --version
```

如果看到了版本号输出，说明安装成功。

### 集成开发环境 (IDE) 设置

虽然 Rust 可以在任何文本编辑器中编写，但使用集成开发环境 (IDE) 可以极大提高开发效率。常用的 Rust IDE 包括：

- **Visual Studio Code**：安装`rust-analyzer`扩展
- **IntelliJ IDEA**：安装`Rust`插件
- **CLion**：由 JetBrains 公司专门为 Rust 开发的 IDE

## Cargo 构建工具

`cargo`是 Rust 官方提供的构建工具和包管理器。它可以帮助我们创建新项目、构建项目、管理依赖等。

### Cargo 项目创建

使用`cargo`创建一个新项目非常简单，只需要在命令行中运行：

```bash
cargo new hello_world
```

这将创建一个名为`hello_world`的新目录，其中包含了一个最小的 Rust 项目结构。

### Cargo 构建和运行

在项目目录中，可以使用`cargo build`命令来构建项目：

```bash
cd hello_world
cargo build
```

构建成功后，可执行文件将被放置在`target/debug`目录中。

要运行程序，可以使用`cargo run`命令：

```bash
cargo run
```

这将自动编译并运行程序。

### Cargo 依赖管理

Rust 使用`Cargo.toml`文件来管理项目依赖。要添加一个新的依赖，只需要在`[dependencies]`部分添加一行即可，例如：

```toml
[dependencies]
rand = "0.8.5"
```

之后运行`cargo build`，`cargo`会自动下载并构建这个依赖。

## Hello World 程序

学习任何一门新语言，第一个程序通常都是`Hello, World!`。让我们来看看如何在 Rust 中实现这个传统。

```rust
fn main() {
    println!("Hello, World!");
}
```

### main 函数

每个 Rust 可执行程序都需要一个`main`函数作为入口点。`fn`关键字用于定义一个函数。

### println! 宏

`println!`是 Rust 中的一个宏，用于将格式化的字符串输出到控制台。在这里，我们只是输出了一个简单的字符串`"Hello, World!"`。

### cargo run

要运行这个程序，我们只需要在项目目录中执行`cargo run`命令即可。`cargo`会自动编译并运行程序，输出结果为`Hello, World!`。

## Rust 基本语法和概念

现在，我们已经了解了如何安装 Rust 环境、使用`cargo`构建工具，并编写了一个简单的`Hello World`程序。接下来，让我们探索一些 Rust
语言的基本语法和概念。

### 变量和不可变性

在 Rust 中，每个变量在声明时都必须指定类型。不过，Rust 也支持类型推导，因此在大多数情况下，你可以省略类型注解。

```rust
let x = 5; // 不可变变量
let mut y = 10; // 可变变量
```

声明变量时使用`let`关键字。如果要让变量可变，需要使用`mut`关键字。

### 数据类型

Rust 是一门静态类型语言，支持以下基本数据类型：

- 标量类型：整数、浮点数、布尔值和字符
- 复合类型：数组和元组

```rust
let x: i32 = 42; // 32 位有符号整数
let y: f64 = 3.14; // 64 位浮点数
let z: bool = true; // 布尔值
let c: char = 'x'; // 字符

let arr: [i32; 5] = [1, 2, 3, 4, 5]; // 数组
let tup: (i32, f64, bool) = (500, 6.28, false); // 元组
```

### 运算符

Rust 支持大多数编程语言中常见的运算符，包括算术运算符、比较运算符、逻辑运算符等。

```rust
let x = 5 + 3 * 2; // x = 11
let y = 10 / 2; // y = 5
let z = x > y; // z = false
```

### 注释

注释是编写代码时非常重要的一部分，它可以帮助我们更好地理解代码的功能和用途。Rust 支持单行注释和多行注释。

```rust
// 这是一个单行注释

/* 这是一个
多行注释 */
```

通过本教程，我相信您已经对 Rust 语言有了初步的了解。当然，这只是一个开始，Rust 还有许多更高级的特性等待您去探索。希望您在学习
Rust 的过程中能够渐入佳境，体会到这门系统编程语言的魅力所在。