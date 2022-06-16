#  SimpleAccumulator

[![Crates.io](https://img.shields.io/crates/v/simple_accumulator)](https://crates.io/crates/simple_accumulator)
[![docs.rs](https://img.shields.io/docsrs/simple_accumulator)](https://docs.rs/simple_accumulator/latest/simple_accumulator/struct.SimpleAccumulator.html)
[![Crates.io](https://img.shields.io/crates/d/simple_accumulator)](https://docs.rs/simple_accumulator/latest/simple_accumulator/struct.SimpleAccumulator.html)

Store and update stats related to our data array without iterating again and again.

**Note:** We calculate approx median(`(min + max + 2*mean)/4`) as to not iterate again and again but you can set the exact one by using 
`calculate_median()`.

Usage: 

```rust
use simple_accumulator::SimpleAccumulator;

fn main() {
    let k = [1, 2, 3, 4];

    // Set field `accumulate` to `false` to not update the field values when
    // changed, you will need to call `calculate_all` to get updated values.
    let mut x = SimpleAccumulator::new(&k, true);

    println!("{:#?}", x);
    
    x.push(5);
    println!("{:#?}", x);

    x.pop();
    println!("{:#?}", x);

    x.remove(2);
    println!("{:#?}", x);
}
```

Output:

```shell
SimpleAccumulator {
    vec: [
        1.0,
        2.0,
        3.0,
        4.0,
    ],
    mean: 2.5,
    population_variance: 1.25,
    standard_deviation: 1.118033988749895,
    min: 1.0,
    max: 4.0,
    median: 2.5,
    len: 4,
    capacity: 4,
    fixed_capacity: false,
    current_write_position: 0,
    accumulate: true,
}
SimpleAccumulator {
    vec: [
        1.0,
        2.0,
        3.0,
        4.0,
        5.0,
    ],
    mean: 3.0,
    population_variance: 1.8,
    standard_deviation: 1.3416407864998738,
    min: 1.0,
    max: 5.0,
    median: 3.0,
    len: 5,
    capacity: 8,
    fixed_capacity: false,
    current_write_position: 0,
    accumulate: true,
}
SimpleAccumulator {
    vec: [
        1.0,
        2.0,
        3.0,
        4.0,
    ],
    mean: 2.5,
    population_variance: 1.25,
    standard_deviation: 1.118033988749895,
    min: 1.0,
    max: 4.0,
    median: 2.5,
    len: 4,
    capacity: 8,
    fixed_capacity: false,
    current_write_position: 0,
    accumulate: true,
}
SimpleAccumulator {
    vec: [
        1.0,
        2.0,
        4.0,
    ],
    mean: 2.3333333333333335,
    population_variance: 1.5833333333333333,
    standard_deviation: 1.2583057392117916,
    min: 1.0,
    max: 4.0,
    median: 2.416666666666667,
    len: 3,
    capacity: 8,
    fixed_capacity: false,
    current_write_position: 0,
    accumulate: true,
}
```