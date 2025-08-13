+++
title = 'The first date between Me and the Rust programming language :)'
date = 2024-01-26T12:06:41+01:00
draft = false
tags=["rust"]
summary="YOOOOOOOOOOOOOOOOOOOOO! In this Im just gonna go through a couple of things I learned going with the Rust book, and it seems pretty interesting so far. It will also serves a documentation for me to remember useful things. Everything will be pretty surface level and just guessing on things because Im going sequentially with the book, thats why im not breaking down things on a deeper level"
+++

##

YOOOOOOOOOOOOOOOOOOOOO!

In this Im just gonna go through a couple of things I learned going with the Rust book, and it seems pretty interesting so far. It will also serves a documentation for me to remember useful things. Everything will be pretty surface level and just guessing on things because Im going sequentially with the book, thats why im not breaking down things on a deeper level.


## First up, Cargo.
Cargo is the build system and the package manager for Rust. Everything compared to C++ feels more modern and I like it.

Cargo.toml is for to define configurations for your packages, for example to include a dependency in your project like random, you have to specify it under your dependencies and then build your project.

Theres also a Cargo.lock file, when you build your project Cargo will see the specified versions there(they are recorded after building). If your project uses 0.8.5 it will remain that until explicitly upgraded.

## Useful cargo commands:

Generating a project (includes gitignore as well):
```cargo new myproject```

To build your project:
```cargo build```

To build and execute a program:
```cargo run```

To check if your code compiles but dont produce and exe:
```cargo check```

Building for release(if you dont use the release flag it will build debug by default):
```cargo build --release```

Updating creates:
```cargo update```

Documentations for packages(generates them locally for you based on the packages you use)(This is legit so insane i fkign love this):
```cargo doc --open```

## Let
First thing first, in the documentation of our first little program, when creating variables we use the ```let``` type, i know nothing so far about it, its probably something similar to c++'s auto, i wonder what exactly happens under the hood, how is it different or better.


## Mutable,immutable
Quoting from the documentation "variables are immutable by default" damn, that is interesting, is it like const?( im comparing things with c++ you can figure it out by now) You use the ```mut``` keyword to make it mutable.

Creating a mutable string:
```let mut mystring = String::new();```

## Including
Syntax for example: ```use std::io;```, but if you didnt include it you could still use ```std::io:stdin``` in your code.

## References
In the example code reference is also used, i wonder is that any different from c++'s.

## Result
If we have a code like this:

```io::stdin().read_line(&mut guess).expect("Failed to read line");```

Readline here returns an enumeration called **Result**, variants are **Ok** and **Err**, err means your operation failed and contains information about how or why. An instance of Result has methods like .expect() you can call.

## Match expression

Im gonna quote this from the documentation its seems pretty serious based on the tone, i should probably be careful saying its just like a switch statement...

"A match expression is made up of **arms**. An arm consists of a **pattern** to match against, and the code that should be run if the value given to match fits that arm’s pattern. 

Rust takes the value given to a match and looks through each arm’s pattern in turn. Patterns and the match construct are powerful Rust features: they let you express a variety of situations your code might encounter and they make sure you handle them all.

Example code:

```
match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
}
```

Notice the **,** at the end of the lines, even at the last one...

## Shadowing

We can create a variable with the same name, it lets us reuse the variable name rather then forcing us to create an other one, useful when reading from stdin and want to convert the input to a number for example.

```
let mut guess = String::new();

io::stdin()
    .read_line(&mut guess)
    .expect("Failed to read line");

let guess: u32 = guess.trim().parse().expect("Please type a number!");
```

## References:
Rust docs: https://doc.rust-lang.org/stable/book/




