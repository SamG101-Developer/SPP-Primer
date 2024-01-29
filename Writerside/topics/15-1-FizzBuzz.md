# 15.1. FizzBuzz

```s++
fun main() -> Void {
    Vec.new_range(0, 100).for_each(fun (x: BigNum) -> Void {
        std.print(case 0 ==
            x % 15 { "FizzBuzz" }
            x % 3 { "Fizz" }
            x % 5 { "Buzz" }
        else { x })
    }
}
```