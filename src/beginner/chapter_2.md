# Rust 语言数据类型全景解析

数据类型是任何编程语言的基石，Rust 作为一种系统级编程语言，对数据类型的设计非常用心。接下来我们就来全面了解一下 Rust
中的数据类型吧。

## 基本数据类型

Rust 将基本数据类型称为"标量"类型，包括整数、浮点数、布尔值和字符。这些标量类型是单个值，是构建更复杂数据类型的基石。

### 整数类型

Rust 整数分为有符号和无符号两种类型：

- **有符号**: `i8`、`i16`、`i32`、`i64`、`i128` 和 `isize`
- **无符号**: `u8`、`u16`、`u32`、`u64`、`u128` 和 `usize`

这些不同的整数类型适用于不同的值范围和占用空间大小。例如，`i32` 是 32 位有符号整数，可表示 -2^31 到 2^31 - 1 范围内的值。

```rust
let x = 98_222;     // 十进制
let y = 0xff;       // 十六进制
let z = 0o77;       // 八进制
let immutable = 5;  // 不可变绑定
```

### 浮点类型

浮点类型用于表示带小数部分的数字，Rust 有两种：

- `f32` 是 32 位浮点数 (单精度)
- `f64` 是 64 位浮点数 (双精度)

```rust
let x = 2.0;   // f64
let y: f32 = 3.14;  // f32
```

### 布尔类型

布尔类型 `bool` 只有两个可能值：`true` 和 `false`。

```rust
let is_ready = true;
let is_valid = false;
```

### 字符类型

Rust 的 `char` 字符类型是一个 Unicode 标量值，占用 4 个字节。

```rust
let c = 'z';
let heart = '♥';
```

## 复合数据类型

复合数据类型可以将多个值组合成单个数据类型。Rust 有两种内置的复合类型：元组和数组。

### 元组

元组是一个固定大小的有序值集合，可以包含不同类型的值。

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
```

可以使用模式匹配来解构元组：

```rust
let (x, y, z) = tup;
println!("x 是 {}", x); // 输出 "x 是 500"
```

### 数组

数组是存放相同类型值的集合，长度固定。

```rust
let arr = [1, 2, 3, 4, 5];
let first = arr[0]; // 1
```

可以这样声明数组类型和长度：

```rust
let arr: [i32; 5] = [1, 2, 3, 4, 5];
```

## 结构体

结构体是自定义的数据类型，可用于将多个不同类型的相关值组合成一个有意义的组合。

```rust
struct Person {
    name: String,
    age: u32,
    is_student: bool,
}

let person = Person {
name: String::from("Alice"),
age: 30,
is_student: false,
};

println!("姓名：{}", person.name);
```

结构体还支持方法定义，使其具有更好的封装性和复用性。

## 枚举

枚举用于在单个类型中定义有限集合的可能值。

```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}

let up = Direction::Up;
```

枚举还可以关联不同类型的数据：

```rust
enum WebEvent {
    PageLoad,
    PageUnload,
    KeyPress(char),
    Paste(String),
    Click { x: i64, y: i64 },
}
```

可以使用 `match` 语句来匹配枚举的不同变体。

通过这个全景教程，相信您已经对 Rust 的基本数据类型和复合数据类型有了全面的理解。Rust
的数据类型设计体现了安全性、简洁性和高效性，是它作为系统级语言的重要基石。下一步，我们将学习 Rust
中的控制流语句，一起继续探索这门优秀语言的更多精彩内容吧！