# 错误处理（Result 和 Option 类型）

## Option 类型

- Option 类型用于处理可能没有值的情况。
- 它是一个枚举，有两种可能的值：Some(T)、None。

```rust
fn divide(numerator: f32, denominator: f32) -> Option<f32> {
    if denominator == 0.0 {
        None
    } else {
        Some(numerator / denominator)
    }
}

fn main() {
    let result = divide(4.0, 2.0);
    let match_result = match result {
        Some(value) => {
            println!("Result: {}", value);
            1
        }
        None => {
            println!("Cannot divide by zero");
            3
        }
    };

    println!("match_result: {:?}", match_result);
}
```

## Result 类型

- Result 类型用于处理可能失败的操作。
- 它是一个枚举，有两种可能的值：Ok(T)和 Err(E)。

```rust
use std::num::ParseIntError;

fn parse_number(str: &str) -> Result<i32, ParseIntError> {
    str.parse::<i32>()
}

fn main() {
    let number = parse_number("42aa");
    match number {
        Ok(value) => println!("Parsed number: {}", value),
        Err(e) => println!("Error parsing number: {}", e),
    }
}
```

## 错误传播

- 使用?运算符可以简化错误传播。
- 是一个语法糖， 相当于 如果 Ok 就返回值， 如果是 Err 就返回 Err 并 return 跳出。

```rust
fn read_file(file_name: &str) -> Result<String, io::Error> {
    let mut file = File::open(file_name)?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}
```

## match 控制流运算符

- match 用于处理 Option 和 Result，使代码清晰且具有表现力。
