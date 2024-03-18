# Rust 模块化编程实战指南

在前面的教程中，我们已经深入探讨了 Rust 模块化编程的各个方面。现在，让我们通过一个实际的项目来实践所学的知识，巩固对 Rust
模块化编程的理解。

在本实战指南中，我们将构建一个简单的命令行工具，用于管理待办事项。这个项目将涉及多个模块，帮助您掌握模块的定义、导入、重导出等技能。

准备好了吗？让我们开始吧！

## 项目设置

首先，让我们创建一个新的 Rust 项目：

```bash
cargo new todo-cli
cd todo-cli
```

这将生成一个基本的项目结构，包括 `src/main.rs` 文件。接下来，我们需要为项目创建一个合适的模块结构。

## 模块结构

我们的待办事项管理工具将包含以下模块：

- `main.rs`: 应用程序的入口点
- `todo/mod.rs`: 定义 Todo 结构体和相关方法
- `cli/mod.rs`: 处理命令行输入/输出
- `storage/mod.rs`: 管理待办事项的存储和加载

在 `src` 目录下，创建这些模块对应的文件和目录：

```
src/
├── main.rs
├── todo/
│   └── mod.rs
├── cli/
│   └── mod.rs
└── storage/
    └── mod.rs
```

现在，让我们在 `main.rs` 中声明这些模块：

```rust
// src/main.rs
mod todo;
mod cli;
mod storage;

fn main() {
    // ...
}
```

通过这种模块化的结构，我们可以更好地组织和管理代码。

## Todo 模块

在 `todo/mod.rs` 文件中，我们定义了一个 `Todo` 结构体，以及一些与待办事项相关的方法。

```rust
// src/todo/mod.rs
pub struct Todo {
    pub description: String,
    pub completed: bool,
}

impl Todo {
    pub fn new(description: &str) -> Self {
        Todo {
            description: description.to_owned(),
            completed: false,
        }
    }

    pub fn toggle(&mut self) {
        self.completed = !self.completed;
    }
}
```

在这个模块中，我们定义了一个公有的 `Todo` 结构体，包含待办事项的描述和完成状态。我们还实现了两个方法：

- `new`: 创建一个新的 `Todo` 实例
- `toggle`: 切换待办事项的完成状态

注意，我们使用了 `pub` 关键字将 `Todo` 结构体和相关方法标记为公有，以便在其他模块中使用。

## CLI 模块

`cli` 模块负责处理命令行输入/输出。让我们在 `cli/mod.rs` 文件中实现一些基本功能。

```rust
// src/cli/mod.rs
use crate::todo::Todo;

pub fn add_todo(description: &str) {
    let todo = Todo::new(description);
    // 存储待办事项
    println!("Added new todo: {}", todo.description);
}

pub fn list_todos() {
    // 加载并列出所有待办事项
}

pub fn toggle_todo(index: usize) {
    // 切换指定索引的待办事项状态
}
```

在这个模块中，我们定义了三个公有函数：

- `add_todo`: 创建一个新的待办事项并存储它
- `list_todos`: 加载并列出所有待办事项
- `toggle_todo`: 切换指定索引的待办事项状态

注意,我们需要从 `crate::todo` 模块导入 `Todo` 结构体,以便在 `add_todo` 函数中使用它。

## Storage 模块

`storage` 模块负责管理待办事项的存储和加载。让我们在 `storage/mod.rs` 文件中实现一些基本功能。

```rust
// src/storage/mod.rs
use crate::todo::Todo;
use std::fs::{File, OpenOptions};
use std::io::{BufReader, BufWriter, Error, ErrorKind};
use std::path::PathBuf;

const DATA_FILE: &str = "todos.data";

pub fn save_todos(todos: &[Todo]) -> Result<(), Error> {
    let path = PathBuf::from(DATA_FILE);
    let file = OpenOptions::new()
        .write(true)
        .create(true)
        .truncate(true)
        .open(&path)?;

    let writer = BufWriter::new(file);

    for todo in todos {
        let line = format!("{}\t{}\n", todo.description, todo.completed);
        writer.write_all(line.as_bytes())?;
    }

    Ok(())
}

pub fn load_todos() -> Result<Vec<Todo>, Error> {
    let path = PathBuf::from(DATA_FILE);
    let file = File::open(&path).map_err(|_| Error::new(ErrorKind::NotFound, "Data file not found"))?;
    let reader = BufReader::new(file);

    let mut todos = Vec::new();

    for line in reader.lines() {
        let line = line?;
        let parts: Vec<&str> = line.split('\t').collect();

        if parts.len() == 2 {
            let description = parts[0].to_owned();
            let completed = parts[1].parse().unwrap_or(false);
            todos.push(Todo {
                description,
                completed,
            });
        }
    }

    Ok(todos)
}
```

在这个模块中，我们定义了两个公有函数：

- `save_todos`: 将待办事项列表保存到文件中
- `load_todos`: 从文件中加载待办事项列表

我们使用了 Rust 的标准库来进行文件操作，包括打开、读取和写入文件。待办事项数据以 `description\tcompleted`
格式存储在文件中，其中 `\t` 是制表符分隔符。

注意,我们需要从 `crate::todo` 模块导入 `Todo` 结构体,以便在 `save_todos` 和 `load_todos` 函数中使用它。

## 集成模块

现在，我们已经实现了所有必需的模块，接下来需要在 `main.rs` 中集成它们。

```rust
// src/main.rs
mod todo;
mod cli;
mod storage;

use cli::{add_todo, list_todos, toggle_todo};
use storage::{load_todos, save_todos};
use std::io;

fn main() {
    let mut todos = load_todos().unwrap_or_default();

    loop {
        println!("请输入命令 (add/list/toggle/exit):");
        let mut input = String::new();
        io::stdin().read_line(&mut input).unwrap();
        let input = input.trim();

        match input {
            "add" => {
                println!("请输入待办事项描述：");
                let mut description = String::new();
                io::stdin().read_line(&mut description).unwrap();
                let description = description.trim();
                add_todo(description);
            }
            "list" => list_todos(),
            "toggle" => {
                println!("请输入待办事项索引：");
                let mut index = String::new();
                io::stdin().read_line(&mut index).unwrap();
                let index = index.trim().parse().unwrap_or(0);
                toggle_todo(index);
            }
            "exit" => break,
            _ => println!("无效命令"),
        }

        save_todos(&todos).unwrap();
    }
}
```

在 `main` 函数中，我们执行以下操作：

1. 从 `cli` 和 `storage` 模块导入所需的函数
2. 加载已保存的待办事项列表
3. 进入一个无限循环，等待用户输入命令
4. 根据用户输入的命令，调用相应的函数
5. 在每次命令执行后，保存更新的待办事项列表

通过这种方式，我们将各个模块集成到应用程序中，实现了基本的待办事项管理功能。

## 运行和测试

现在，我们可以运行应用程序并进行测试了。在项目根目录下执行以下命令：

```bash
cargo run
```

您应该会看到以下输出：

```
请输入命令 (add/list/toggle/exit):
```

尝试输入不同的命令，如 `add`、`list`、`toggle` 和 `exit`,测试应用程序的各个功能。

## 总结

通过本实战指南，我们构建了一个简单的命令行工具，并实践了 Rust
模块化编程的各个方面，包括模块定义、导入、重导出等。我们还学习了如何合理地组织模块结构，以及如何在不同模块之间共享数据和功能。

虽然这是一个简单的示例，但它展示了 Rust 模块化编程的强大功能，以及如何利用这些功能构建可维护和可扩展的应用程序。无论您是开发系统级软件、Web
应用程序还是游戏，都可以运用这些技能来组织和管理代码。

现在，您已经掌握了 Rust 模块化编程的实战技能。继续探索和实践吧，尽情发挥您的创造力！