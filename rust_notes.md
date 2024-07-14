
# Rust 学习笔记

## 第三章：常见编程概念

### 3.1 变量与可变性

#### 变量声明
- **声明变量**：使用 `let` 关键字创建变量。默认情况下，Rust 中的变量是不可变的（immutable）。
  ```rust
  let x = 5;
  ```

#### 可变变量
- **可变变量**：使用 `let mut` 关键字声明可变变量，允许对变量的值进行修改。
  ```rust
  let mut x = 5;
  x = 6;
  ```

#### 常量
- **常量声明**：使用 `const` 关键字声明常量，必须显式指定类型，常量在整个程序运行期间保持不变。
  ```rust
  const MAX_POINTS: u32 = 100_000;
  ```

#### 变量遮蔽（Shadowing）
- **遮蔽**：允许在同一作用域内声明同名变量，新变量会遮蔽（覆盖）旧变量。新的变量可以改变类型，并且是不可变的。
  ```rust
  let x = 5;
  let x = x + 1;
  let x = "six"; // 变量 x 的类型从整数变为字符串
  ```

#### 不可变性的重要性
- **不可变性**：默认不可变性帮助防止数据竞争，确保线程安全，提高代码的可读性和可维护性。

### 示例代码
```rust
fn main() {
    // 不可变变量
    let x = 5;
    println!("The value of x is: {}", x);

    // 可变变量
    let mut y = 5;
    println!("The value of y is: {}", y);
    y = 6;
    println!("The value of y is: {}", y);

    // 常量
    const MAX_POINTS: u32 = 100_000;
    println!("The maximum points are: {}", MAX_POINTS);

    // 变量遮蔽
    let z = 5;
    let z = z + 1;
    let z = "six";
    println!("The value of z is: {}", z);
}
```

### 关键点总结
1. **不可变变量**：默认不可变，确保安全性。
2. **可变变量**：使用 `mut` 声明，可修改。
3. **常量**：使用 `const` 声明，需显式类型，全局不变。
4. **遮蔽**：允许重复使用变量名，改变变量类型或值。

### 优势
- **安全性**：默认不可变变量防止数据竞争，确保线程安全。
- **可读性**：代码更容易理解和维护。
- **灵活性**：通过遮蔽和可变变量，提供了灵活的数据处理方式。

## 3.2 数据类型

#### 标量类型 (Scalar Types)
- **整型 (Integer Types)**：用于存储整数。根据大小和符号分为多种类型，如 `i8`, `u8`, `i32`, `u32`, `i64`, `u64` 等。
  - **符号**：`i` 表示有符号，`u` 表示无符号。
  - **大小**：数字表示位数，如 `8` 表示 8 位，`32` 表示 32 位。
  - **示例**：
    ```rust
    let x: i32 = 42;
    let y: u64 = 100;
    ```

- **浮点型 (Floating-Point Types)**：用于存储小数。主要有 `f32` 和 `f64` 两种类型，分别表示 32 位和 64 位浮点数。
  - **示例**：
    ```rust
    let x: f32 = 3.14;
    let y: f64 = 2.71828;
    ```

- **布尔型 (Boolean Type)**：用于存储布尔值，只有两个可能的值：`true` 和 `false`。
  - **示例**：
    ```rust
    let is_rust_fun: bool = true;
    ```

- **字符型 (Character Type)**：用于存储单个 Unicode 字符。表示方式为单引号括起来的字符，如 `'a'`, `'字'`。
  - **示例**：
    ```rust
    let letter: char = 'z';
    let emoji: char = '😊';
    ```

#### 复合类型 (Compound Types)
- **元组 (Tuples)**：将多个值组合在一起，可以包含不同类型的值。元组的长度是固定的。
  - **声明和访问**：
    ```rust
    let tup: (i32, f64, u8) = (500, 6.4, 1);
    let (x, y, z) = tup;
    println!("The value of y is: {}", y);
    ```
  - **通过索引访问**：
    ```rust
    let five_hundred = tup.0;
    let six_point_four = tup.1;
    let one = tup.2;
    ```

- **数组 (Arrays)**：将多个相同类型的值组合在一起。数组的长度是固定的，声明时必须指定长度。
  - **声明和访问**：
    ```rust
    let a = [1, 2, 3, 4, 5];
    let first = a[0];
    let second = a[1];
    ```
  - **数组的类型和长度**：
    ```rust
    let b: [i32; 5] = [1, 2, 3, 4, 5];
    ```

### 关键点总结
1. **整型和浮点型**：用于存储整数和小数，具有不同大小和符号。
2. **布尔型和字符型**：用于存储布尔值和单个字符。
3. **元组**：组合多种类型的固定长度数据。
4. **数组**：组合相同类型的固定长度数据。

### 优势
- **类型安全**：Rust 强类型系统确保数据类型的正确性，防止类型错误。
- **灵活性**：支持多种标量和复合类型，适应不同的编程需求。
- **性能优化**：通过固定长度的复合类型（如元组和数组），提高内存和运行效率。

## 3.3 函数

#### 函数的定义和调用
- **定义函数**：使用 `fn` 关键字定义函数。函数名通常使用蛇形命名法（snake_case）。
  ```rust
  fn main() {
      println!("Hello, world!");
  }
  ```
- **函数参数**：函数可以有多个参数，每个参数需要显式指定类型。
  ```rust
  fn print_value(x: i32) {
      println!("The value is: {}", x);
  }
  ```

#### 返回值
- **返回值类型**：使用箭头 `->` 指定返回值类型。Rust 函数的返回值是表达式而不是语句，因此不用写 `return` 关键字。
  ```rust
  fn five() -> i32 {
      5
  }
  ```
- **带返回值的函数**：
  ```rust
  fn add(x: i32, y: i32) -> i32 {
      x + y
  }
  ```

#### 语句与表达式
- **语句**：执行一些操作但不返回值。例如，变量声明是一个语句。
  ```rust
  let y = 6;
  ```
- **表达式**：计算并返回一个值。函数体内的代码块也是一个表达式。
  ```rust
  let x = 5;
  let y = {
      let x = 3;
      x + 1
  }; // y的值是4
  ```

#### 函数调用
- **调用函数**：通过函数名和参数列表调用函数。
  ```rust
  fn main() {
      let result = add(5, 6);
      println!("The result is: {}", result);
  }
  ```

### 示例代码
```rust
fn main() {
    println!("Hello, world!");

    print_value(10);

    let sum = add(5, 3);
    println!("Sum: {}", sum);

    let num = five();
    println!("Number: {}", num);
}

fn print_value(x: i32) {
    println!("The value is: {}", x);
}

fn add(x: i32, y: i32) -> i32 {
    x + y
}

fn five() -> i32 {
    5
}
```

### 关键点总结
1. **函数定义**：使用 `fn` 关键字，明确参数和返回值类型。
2. **返回值**：使用箭头 `->` 指定返回值类型，最后一个表达式即为返回值。
3. **语句与表达式**：语句不返回值，表达式返回值，函数体内代码块为表达式。
4. **函数调用**：通过函数名和参数列表进行调用。

## 3.4 注释

#### 单行注释
- **单行注释**：使用 `//` 开始单行注释，注释内容从 `//` 开始到行末结束。
  ```rust
  // 这是一个单行注释
  let x = 5; // 这也是一个单行注释
  ```

#### 多行注释
- **多行注释**：使用 `/* */` 包裹多行注释，注释内容可以跨越多行。
  ```rust
  /* 这是一个多行注释
     它可以跨越多行 */
  let x = 5;
  ```

#### 文档注释
- **文档注释**：用于生成文档，单行文档注释使用 `///`，多行文档注释使用 `/** */`。文档注释通常写在函数、结构体等前面。
  ```rust
  /// 这是一个文档注释
  /// 它用于描述接下来的函数
  fn add(x: i32, y: i32) -> i32 {
      x + y
  }
  ```

### 示例代码
```rust
fn main() {
    // 打印 "Hello, world!"
    println!("Hello, world!");

    let x = 5; // 定义一个变量 x 并赋值为 5

    /* 这是一个多行注释
       它可以跨越多行 */
    let y = 10; // 定义一个变量 y 并赋值为 10

    /// 这是一个文档注释
    /// 它用于描述接下来的函数
    fn add(x: i32, y: i32) -> i32 {
        x + y
    }

    let sum = add(x, y);
    println!("Sum: {}", sum);
}
```

### 关键点总结
1. **单行注释**：使用 `//`，适用于简短的注释。
2. **多行注释**：使用 `/* */`，适用于较长的注释。
3. **文档注释**：使用 `///` 或 `/** */`，用于生成文档，描述函数、结构体等。

### 优势
- **可读性**：注释提高代码的可读性和可维护性，帮助理解代码逻辑。
- **文档生成**：文档注释可以自动生成文档，方便维护和使用。
- **调试和测试**：注释可以临时屏蔽代码，方便调试和测试。

## 3.5 控制流

#### if 表达式
- **基本结构**：使用 `if` 关键字进行条件判断。
  ```rust
  let number = 5;

  if number < 10 {
      println!("The number is less than 10");
  } else {
      println!("The number is greater than or equal to 10");
  }
  ```
- **if-else if**：多条件判断。
  ```rust
  let number = 6;

  if number % 4 == 0 {
      println!("The number is divisible by 4");
  } else if number % 3 == 0 {
      println!("The number is divisible by 3");
  } else if number % 2 == 0 {
      println!("The number is divisible by 2");
  } else {
      println!("The number is not divisible by 4, 3, or 2");
  }
  ```

#### 循环
- **loop**：创建无限循环，使用 `break` 退出循环。
  ```rust
  loop {
      println!("This will print forever");
      break; // 退出循环
  }
  ```

- **while**：在条件为真时循环。
  ```rust
  let mut number = 3;

  while number != 0 {
      println!("{}", number);
      number -= 1;
  }
  ```

- **for**：遍历集合中的每一个元素。
  ```rust
  let a = [10, 20, 30, 40, 50];

  for element in a.iter() {
      println!("The value is: {}", element);
  }
  ```

#### Range 语法
- **Range**：创建一个范围，使用 `..` 和 `..=` 语法。
  ```rust
  for number in 1..4 {
      println!("{}", number);
  }

  for number in 1..=4 {
      println!("{}", number);
  }
  ```

### 示例代码
```rust
fn main() {
    // if 表达式
    let number = 6;

    if number % 4 == 0 {
        println!("The number is divisible by 4");
    } else if number % 3 == 0 {
        println!("The number is divisible by 3");
    } else if number % 2 == 0 {
        println!("The number is divisible by 2");
    } else {
        println!("The number is not divisible by 4, 3, or 2");
    }

    // loop 循环
    let mut count = 0;

    loop {
        count += 1;
        if count == 3 {
            break;
        }
    }

    // while 循环
    let mut number = 3;

    while number != 0 {
        println!("{}!", number);
        number -= 1;
    }

    // for 循环
    let a = [10, 20, 30, 40, 50];

    for element in a.iter() {
        println!("The value is: {}", element);
    }

    // Range 语法
    for number in 1..4 {
        println!("{}", number); // 打印 1, 2, 3
    }

    for number in 1..=4 {
        println!("{}", number); // 打印 1, 2, 3, 4
    }
}
```

### 关键点总结
1. **if 表达式**：进行条件判断。
2. **loop 循环**：创建无限循环，使用 `break` 退出。
3. **while 循环**：在条件为真时执行循环。
4. **for 循环**：遍历集合中的元素。
5. **Range 语法**：创建范围，用于循环遍历。

### 优势
- **灵活性**：多种控制流结构适应不同的编程需求。
- **安全性**：通过显式的条件判断和循环控制，提高代码的可读性和安全性。
- **简洁性**：使用简洁的语法进行复杂的控制流操作。

### 优势
- **内存效率**：Slice 不复制数据，仅借用一部分，节省内存。
- **灵活性**：Slice 使函数更通用，可以处理不同类型和长度的数据。
- **安全性**：Rust 确保 Slice 的引用安全，防止悬垂引用和内存泄漏。
