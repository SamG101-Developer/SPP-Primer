# 6.1. Arrays
Arrays in S++ use the 1st class type `Arr[T]`. This allows the language to remain orthogonal, as there is no special 
behaviours / restrictions, unlike C++'s `T[]` arrays. Arrays are fixed size, and map to LLVM's array type. All 
operations on arrays are bounds-checked, ensuring that no out-of-bounds accesses can ever occur.

## Array syntax
Arrays have the `[...]` literal that can be used to easily create arrays. Because of the type-system not allowing 
types to be declared on the lhs, for an empty array the type is included in the array declaration:

#### Array syntax example (literal)
```s++
fun main() -> Void {
    let x = [1, 2, 3]  # x: Arr[BigNum]
    let y = [Str]      # y: Arr[Str]
}
```

#### Array syntax example (method)
```s++
fun main() -> Void {
    let x = Arr.new(1, 2, 3)  # x: Arr[BigDec]
    let y = Arr[Str].new()    # y: Arr[Str]
}
```

## Array API
```s++
cls Arr[T] {
    @private data: std.c.CArr[T]
    @private len : U64
}

sup [T] Arr[T] {
    use Item = T
    
    fun get(&self, i: U256) -> Ret[Self.Item, BoundsErr] { ... }
    fun set(&mut self, i: U256, value: Self.Item) -> Ret[Void, BoundsErr] { ... }
    fun del(&mut self, i: U256) -> Ret[Void, BoundsErr] { ... }
    fun has(&self, i: U256) -> Bool { ... }
    fun len(&self) -> U256 { ... }
}
```
Other classes are superimposed onto `Arr[T]` to provide the rest of the API. The `Arr[T]` type is a wrapper around a
C array, which is stack allocated.
