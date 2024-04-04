# 5.4. Generics

## Generic parameter classifications
Generic parameters, like function parameters, have a number of classifications. These are:

## Usage & Inference

## Generic constraints

## Specialization

## Void
The `Void` type can be used as a generic argument for a generic parameter, but cannot be used for a class attribute 
type. This is because representing the absence of a value is not possible in S++. Using `Void` as a parameter type 
removes the parameter from the overload being considered. This is seen a lot in the `Gen.next(value: Send)` method of 
the `Gen` class, as the parameter type is the `Send` generic parameter of the `Gen` class, but defaults to 
`Send=Void`, meaning that a lot of the time, `.next()` doesn't take an argument.
