# Rust 入门篇：从基础到实践

--- 

一、语言基础概念

Rust 是一种系统编程语言，专注于性能、并发和安全性。它的主要目标是帮助开发人员编写高效、可靠和安全的软件。Rust
采用了独特的所有权 (Ownership) 和借用 (Borrowing) 概念来管理内存，避免了常见的内存错误，如空指针和数据竞争。

二、开发环境搭建

1. 安装 Rust

    - 访问 https://www.rust-lang.org/tools/install 并根据您的操作系统选择安装程序。

2. 更新 Rust

    - `rustup update`

3. 构建 Hello World 项目
    - `cargo new hello_world`
    - `cd hello_world`

三、第一个程序

`hello_world/src/main.rs`

```rust
fn main() {
    println!("Hello, world!");
}
```

- `fn main() { ... }` 是程序的入口点
- `println!` 是一个宏，用于打印输出

运行：

- `cargo run`

四、基础语法

1. 变量

    - `let x = 5;` (不可变)
    - `let mut y = 5;` (可变)

2. 函数

   ```rust
   fn add(x: i32, y: i32) -> i32 {
       x + y
   }
   ```

3. 注释

    - `// 单行注释`
    - `/* 多行注释 */`

4. 结构体

   ```rust
   struct Person {
       name: String,
       age: u32,
   }
   ```

5. 枚举
   ```rust
   enum Color {
       Red,
       Green,
       Blue,
   }
   ```

五、数据类型

1. 基础类型

    - 标量类型：整数、浮点数、布尔值、字符
    - 复合类型：元组、数组

2. 字符串

    - `String` - 可增长的字符串
    - `&str` - 字符串切片

3. 所有权和借用
    - 每个值都有一个所有者
    - 当所有者离开作用域时，值将被丢弃
    - 借用是对值的引用，不拥有所有权

六、流程控制

1. `if` 条件语句

   ```rust
   let x = 5;
   if x > 0 {
       println!("x is positive");
   } else {
       println!("x is negative or zero");
   }
   ```

2. `loop`

   ```rust
   let mut count = 0;
   loop {
       count += 1;
       if count == 5 {
           break;
       }
   }
   ```

3. `for` 循环

    - 遍历集合

      ```rust
      let nums = [1, 2, 3];
      for n in nums.iter() {
          println!("{}", n);
      }
      ```

    - 范围
      ```rust
      for i in 0..5 {
          println!("{}", i); // 0 1 2 3 4
      }
      ```

这只是 Rust 入门的冰山一角，还有许多其他重要的概念和主题需要学习，如所有权和借用、模块系统、trait、生命周期、并发编程等。希望这个总结对您入门
Rust 有所帮助！如有任何疑问，欢迎随时询问。