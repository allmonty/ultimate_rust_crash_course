# Exercise A: Variables

### Part 1
- [x] Make a new project named `variables` using cargo
  - See "cargo help" if you forgot the command.
- [x] Open `Cargo.toml`
  - Hopefully Rust was able to figure out your name and email address for you!
  - [x] Change the version number to `2.3.4`, just for fun, and save the file.
    Keep an eye out for that version number in cargo's output when you run it!
    ```sh
    ➜  variables git:(master) ✗ cargo run
      Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
        Finished dev [unoptimized + debuginfo] target(s) in 2.13s
        Running `target/debug/variables`
    Hello, world!
    ```
- [x] In `src/main.rs`
  - [x] Declare the variable `missiles` and initialize it to `8`
  - [x] Declare the variable `ready` and initialize it to `2`
- [x] Change the `println!(...)` at the end of `main()` to:
  - `println!("Firing {} of my {} missiles...", ready, missiles);`
- [x] Run your program using cargo (see "cargo help" if you forgot the command).
  Some common errors you may hit:
  - Forgot to use `let` to bind a variable
  - Forgot a semicolon `;` at the end of each line
  ```sh
  ➜  variables git:(master) ✗ cargo run
    Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
      Finished dev [unoptimized + debuginfo] target(s) in 0.20s
      Running `target/debug/variables`
  Firing 2 of my 8 missiles...
  ```

### Part 2

- [x] After the first `println!(...)`, subtract `ready` from `missiles` like this:
  - `missiles = missiles - ready;`
- [x] Add a second `println!(...)` to the end:
  - `println!("{} missiles left", missiles);`
- [x] Run your program again using cargo
  - Did you run into an error about mutability?  Make sure you added `mut` to the right place.
  ```sh
  ➜  variables git:(resolution) cargo run
    Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
  error[E0384]: cannot assign twice to immutable variable `missiles`
  --> src/main.rs:5:5
    |
  2 |     let missiles = 8;
    |         --------
    |         |
    |         first assignment to `missiles`
    |         help: make this binding mutable: `mut missiles`
  ...
  5 |     missiles = missiles - ready;
    |     ^^^^^^^^^^^^^^^^^^^^^^^^^^^ cannot assign twice to immutable variable

  error: aborting due to previous error

  For more information about this error, try `rustc --explain E0384`.
  error: could not compile `variables`.

  To learn more, run the command again with --verbose.
  ```
- [x] Declare a constant named `STARTING_MISSILES` and set it to `8` (the type is `i32`).
- [x] Declare a constant named `READY_AMOUNT` and set it to `2` (also `i32`).
- [x] Use the constants to initialize `missiles` and `ready`
  - Where did you put the constants?  If you put them in `main()`, try moving them up above main at module scope! 
- [x] Nice. Congratulate yourself on a job well done!  You are a Rust programmer now!

### Extra challenges:
- [x] Explicitly annotate the variables with the type `i32`
- [x] Try binding the variables all at once on one line using a pattern (parenthesis and commas) -- can you figure out where "mut" goes?
  - [x] Can you figure out the correct type annotation when you assign them all in one line?
    Hint: it will use the same sort of pattern as the variables and values.
- [x] Instead of changing missiles, use the value `missiles - ready` directly in the second `println!(...)`
  - What does cargo say when you run your program?
    ```sh
    ➜  variables git:(resolution) ✗ cargo run
    Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
    warning: variable does not need to be mutable
    --> src/main.rs:5:10
      |
    5 |     let (mut missiles, ready) : (i32, i32) = (STARTING_MISSILES, READY_AMOUNT);
      |          ----^^^^^^^^
      |          |
      |          help: remove this `mut`
      |
      = note: `#[warn(unused_mut)]` on by default

    warning: 1 warning emitted

        Finished dev [unoptimized + debuginfo] target(s) in 0.21s
        Running `target/debug/variables`
    Firing 2 of my 8 missiles...
    6 missiles left
    ```
- [x] Add another variable to your program *but don't use it*.
  - What does cargo say when you run your program?
  ```sh
  ➜  variables git:(resolution) ✗ cargo run
    Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
  warning: unused variable: `not_used`
  --> src/main.rs:8:9
    |
  8 |     let not_used = 1;
    |         ^^^^^^^^ help: if this is intentional, prefix it with an underscore: `_not_used`
    |
    = note: `#[warn(unused_variables)]` on by default

  warning: variable does not need to be mutable
  --> src/main.rs:5:10
    |
  5 |     let (mut missiles, ready) : (i32, i32) = (STARTING_MISSILES, READY_AMOUNT);
    |          ----^^^^^^^^
    |          |
    |          help: remove this `mut`
    |
    = note: `#[warn(unused_mut)]` on by default

  warning: 2 warnings emitted

      Finished dev [unoptimized + debuginfo] target(s) in 0.21s
      Running `target/debug/variables`
  Firing 2 of my 8 missiles...
  6 missiles left
  ```
- [x] Try modifying a constant in `main()` (for example, `READY_AMOUNT = 1`). What does the error look like?
  ```sh
  ➜  variables git:(resolution) ✗ cargo run
    Compiling variables v2.3.4 (/Users/allan.david/dev/personal/ultimate_rust_crash_course/exercise/a-variables/variables)
  error[E0070]: invalid left-hand side of assignment
  --> src/main.rs:9:23
    |
  9 |     STARTING_MISSILES = 10;
    |     ----------------- ^
    |     |
    |     cannot assign to this expression

  error: aborting due to previous error

  For more information about this error, try `rustc --explain E0070`.
  error: could not compile `variables`.

  To learn more, run the command again with --verbose.
  ```
