1.

```rust
use std::fmt;

struct Point {
    x: i32,
    y: i32,
}

impl fmt::Display for Point {
    // IMPLEMENT fmt method
    fn fmt(&self, f:&mut fmt::Formatter<'_>) -> fmt::Result{
        write!(f,"The point is ({}, {})",self.x, self.y)
    }
}

fn main() {
    let origin = Point { x: 0, y: 0 };
    // FILL in the blanks
    assert_eq!(origin.to_string(), "The point is (0, 0)");
    assert_eq!(format!("{}", origin), "The point is (0, 0)");

    println!("Success!")
}


```

2.

```rust
// To use `from_str` method, you needs to introduce this trait into the current scope.
use std::str::FromStr;
fn main() {
    let parsed: i32 = "5".parse().unwrap();
    let turbo_parsed: i32 = "10".parse().unwrap();
    let from_str: i32 = "20".parse().unwrap();
    let sum = parsed + turbo_parsed + from_str;
    assert_eq!(sum, 35);

    println!("Success!")
}

```

3.

```rust
use std::str::FromStr;
use std::num::ParseIntError;

#[derive(Debug, PartialEq)]
struct Point {
    x: i32,
    y: i32
}

impl FromStr for Point {
    type Err = ParseIntError;

    fn from_str(s: &str) -> Result<Self, Self::Err> {
        let coords: Vec<&str> = s.trim_matches(|p| p == '(' || p == ')' )
                                 .split(',')
                                 .collect(); //splitting the string by () and collecting the points

        let x_fromstr = coords[0].parse::<i32>()?;
        let y_fromstr = coords[1].parse::<i32>()?;

        Ok(Point { x: x_fromstr, y: y_fromstr })
    }
}
fn main() {
    // FILL in the blanks in two ways
    // DON'T change code anywhere else 
    let p = Point::from_str("(3,4)");
    assert_eq!(p.unwrap(), Point{ x: 3, y: 4} );

    println!("Success!")
}

```

4.

```rust


```