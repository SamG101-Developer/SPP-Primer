# 9.2. Error Handling & Opt/Ret

Error handling in S++ is done similarly to in Rust, using monadic error handling. The `Ret` (for return) type is used,
as it can hold a pass and fail state. The `Opt` (for optional) type is used to hold a value that may or may not 
exist. Because [linear types] are enforced, it means that the error of a `Ret` type must be handled (which includes 
propagating it up the call stack), forcing the programmer to handle errors and preventing them from being ignored.