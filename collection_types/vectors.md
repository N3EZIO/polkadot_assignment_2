1.

```rust

fn main() {
    let arr: [u8; 3] = [1, 2, 3];
    
    let v = Vec::from(arr);
    is_vec(&v);

    let v = &vec![1, 2, 3];
    is_vec(v);

    // vec!(..) and vec![..] are same macros, so
    let v = &vec!(1, 2, 3);
    is_vec(v);
    
    // in code below, v is Vec<[u8; 3]> , not Vec<u8>
    // USE Vec::new and `for` to rewrite the below code 
    let mut v1 = Vec::new();
    for i in &arr{
        v1.push(*i);
    }
    is_vec(&v1);
 
    assert_eq!(*v, v1);

    println!("Success!")
}

fn is_vec(v: &Vec<u8>) {}

```



3.
```rust

// FILL in the blanks
fn main() {
    // array -> Vec
    // impl From<[T; N]> for Vec
    let arr = [1, 2, 3];
    let v1 = Vec::from(arr);
    let v2: Vec<i32> = arr.into_iter().collect();
 
    assert_eq!(v1, v2);
 
    
    // String -> Vec
    // impl From<String> for Vec
    let s = "hello".to_string();
    let v1: Vec<u8> = s.as_bytes().to_vec(); //converting to bytes then converting vec

    let s = "hello".to_string();
    let v2 = s.into_bytes();
    assert_eq!(v1, v2);

    // impl<'_> From<&'_ str> for Vec
    let s = "hello";
    let v3 = Vec::from(s); //getting vector from String
    assert_eq!(v2, v3);

    // Iterators can be collected into vectors
    let v4: Vec<i32> = [0; 10].into_iter().collect();
    assert_eq!(v4, vec![0; 10]);

    println!("Success!")
 }

```

4.

```rust
// FIX the error and IMPLEMENT the code
fn main() {
    let mut v = Vec::from([1, 2, 3]);
    for i in 0..3 {
        println!("{:?}", v[i])
    }

    for i in 0..5 {
       // IMPLEMENT the code here...
       if i >= v.len(){
           v.push(i+2);
       }else{
           v[i] += 1;
       }
    }
    
    assert_eq!(v, vec![2, 3, 4, 5, 6]);

    println!("Success!")
}
```

5.
```rust

// FIX the errors
fn main() {
    let mut v = vec![1, 2, 3];

    let slice1 = &v[..];
    // out of bounds will cause a panic
    // You must use `v.len` here
    let slice2 = &v[0..v.len()];
    
    assert_eq!(slice1, slice2);
    
    // slice are read only
    // Note: slice and &Vec are different
    let vec_ref: &mut Vec<i32> = &mut v;
    (*vec_ref).push(4);
    let slice3 = &mut vec_ref[0..4];
    // slice3.push(4)

    assert_eq!(slice3, &[1, 2, 3, 4]);

    println!("Success!")
}

```

6.

```rust
// FIX the errors
fn main() {
    let mut vec = Vec::with_capacity(10);

    // The vector contains no items, even though it has capacity for more
    assert_eq!(vec.len(), 0);
    assert_eq!(vec.capacity(), 10);

    // These are all done without reallocating...
    for i in 0..10 {
        vec.push(i);
    }
    assert_eq!(vec.len(), 10);
    assert_eq!(vec.capacity(), 10);

    // ...but this may make the vector reallocate
    vec.push(11);
    assert_eq!(vec.len(), 11);
    assert!(vec.capacity() >= 11);


    // fill in an appropriate value to make the `for` done without reallocating 
    let mut vec = Vec::with_capacity(100);
    for i in 0..100 {
        vec.push(i);
    }

    assert_eq!(vec.len(), 100);
    assert_eq!(vec.capacity(), 100);
    
    println!("Success!")
}

```

7.
```rust
#[derive(Debug, PartialEq, Clone)] //Clone trait has to be used too assign the values to v
enum IpAddr {
    V4(String),
    V6(String),
}
fn main() {
    // FILL in the blank
    let v : Vec<IpAddr>= [IpAddr::V4("127.0.0.1".to_string()), IpAddr::V6("::1".to_string())].to_vec();
    
    // Comparing two enums need to derive the PartialEq trait
    assert_eq!(v[0], IpAddr::V4("127.0.0.1".to_string()));
    assert_eq!(v[1], IpAddr::V6("::1".to_string()));

    println!("Success!")
}

```

8.
```rust
trait IpAddr {
    fn display(&self);
}

struct V4(String);
impl IpAddr for V4 {
    fn display(&self) {
        println!("ipv4: {:?}",self.0)
    }
}
struct V6(String);
impl IpAddr for V6 {
    fn display(&self) {
        println!("ipv6: {:?}",self.0)
    }
}

fn main() {
    // FILL in the blank
    let v: Vec<Box <dyn IpAddr>>= vec![ //The dataype is Box and should contain that has the IpAddr trait
        Box::new(V4("127.0.0.1".to_string())),
        Box::new(V6("::1".to_string())),
    ];

    for ip in v {
        ip.display();
    }
}

```