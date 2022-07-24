1. 

```rust
struct Array<T, const N: usize> {
    data : [T; N]
}

fn main() {
    let arrays = [
        Array::<i32,3>{
            data: [1, 2, 3],
        },
        Array::<i32, 3>{
            data: [1, 2, 3], //in an array(matrix here) only arrays of same type can be stored. Therefore, have to convert from f32 to i32
        },
        Array::<i32, 3> {
            data: [1,5, 2]
        }
    ];

    println!("Success!");
}

```

2.
```rust

// Fill in the blanks to make it work.
fn print_array<T: std::fmt::Debug, const n:usize>(arr: [T; n]) {
    println!("{:?}", arr);
}
fn main() {
    let arr = [1, 2, 3];
    print_array(arr);

    let arr = ["hello", "world"];
    print_array(arr);
}

```


3.
```rust
#![allow(incomplete_features)]
#![feature(generic_const_exprs)]

fn check_size<T>(val: T)
where
    Assert<{ core::mem::size_of::<T>() < 768 }>: IsTrue,
{
    //...
}

// Fix the errors in main.
fn main() {
    check_size([0u8; 762]); 
    check_size([0i32; 191]);
    check_size(["hello你好"; 47]); // Size of &str // size of each slice is 16 (pointer and length). 768/16 = 47 
    check_size([(); 31].map(|_| "hello你好".to_string()));  // Size of String? smart pointer size is 24 and 768/24 = 32
    check_size(['中'; 191]); // Size of char ? //each char is 4bytes

    println!("Success!");
}



pub enum Assert<const CHECK: bool> {}

pub trait IsTrue {}

impl IsTrue for Assert<true> {}

```