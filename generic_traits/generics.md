```rust


// Fill in the blanks to make it work
struct A;          // Concrete type `A`.
struct S(A);       // Concrete type `S`.
struct SGen<T>(T); // Generic type `SGen`.

fn reg_fn(_s: S) {}

fn gen_spec_t(_s: SGen<A>) {}

fn gen_spec_i32(_s: SGen<i32>) {}

fn generic<T>(_s: SGen<T>) {}

fn main() {
    // Using the non-generic functions
    reg_fn(S(A));          // Concrete type. A is a concrete type reg_fn except type S and the struct S expects A.
    gen_spec_t(SGen(A));   // Implicitly specified type parameter `A`. SGen accepts a generic type but gen_spec_t expects SGen(A)
    gen_spec_i32(SGen(9)); // Implicitly specified type parameter `i32`.

    // Explicitly specified type parameter `char` to `generic()`.
    generic::<char>(SGen('x'));

    // Implicitly specified type parameter `char` to `generic()`.
    generic(SGen('c'));

    println!("Success!");
}

```


```rust

// Implement the generic function below.
fn sum<T: std::ops::Add<Output = T>>(s: T, y: T) -> T {
    s + y
}

fn main() {
    assert_eq!(5, sum(2i8, 3i8));
    assert_eq!(50, sum(20, 30));
    assert_eq!(2.46, sum(1.23, 1.23));

    println!("Success!");
}

```


```rust

// Implement struct Point to make it work.
struct Point<T>{
    x: T,
    y: T
}

fn main() {
    let integer = Point { x: 5, y: 10 };
    let float = Point { x: 1.0, y: 4.0 };

    println!("Success!");
}

```


```rust

// Modify this struct to make the code work
struct Point<T, C> { //defining another generic type C
    x: T,
    y: C,
}

fn main() {
    // DON'T modify this code.
    let p = Point{x: 5, y : "hello".to_string()};

    println!("Success!");
}

```


```rust

// Add generic for Val to make the code work, DON'T modify the code in `main`.
struct Val<T> {
    val: T,
}

impl<T> Val<T>{  //implementation of type generic and implementing a struct as generic
    fn value(&self) -> &T {  // no need to mention <T> here
        &self.val
    }
}


fn main() {
    let x = Val{ val: 3.0 };
    let y = Val{ val: "hello".to_string()};
    println!("{}, {}", x.value(), y.value());
}

```


```rust
struct Point<T, U> {
    x: T,
    y: U,
}

impl<T, U> Point<T, U> {
    // Implement mixup to make it work, DON'T modify other code.
    fn mixup<V,W>(self, P:Point<V,W>) -> Point<T,W>{ // type T is from self type W is from y
        Point{
            x: self.x,
            y: P.y
        }
    }
}

fn main() {
    let p1 = Point { x: 5, y: 10 };
    let p2 = Point { x: "Hello", y: '中'};

    let p3 = p1.mixup(p2);

    assert_eq!(p3.x, 5);
    assert_eq!(p3.y, '中');

    println!("Success!");
}

```


```rust

// Fix the errors to make the code work.
struct Point<T> {
    x: T,
    y: T,
}

impl Point<i32> {
    fn distance_from_origin(&self) -> f32 {
        (((self.x)as f32) .powi(2) + ((self.y) as f32).powi(2)).sqrt()
    }
}

fn main() {
    let p = Point{x: 5, y: 10};
    println!("{}",p.distance_from_origin());
}

```


