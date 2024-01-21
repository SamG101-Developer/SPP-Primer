# 9.2. Error Handling & Opt/Ret

Error handling in S++ is done similarly to in Rust, using monadic error handling. The `Ret` (for return) type is used,
as it can hold a pass and fail state. The `Opt` (for optional) type is used to hold a value that may or may not exist.