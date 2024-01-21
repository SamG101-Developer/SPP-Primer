# 3.5. Basic I/O

IO is split into a few major categories: file IO, console IO, and network IO. Each set of IO has its own namespaced 
functions, but there are some aliases to make it easier to use. For example, `std.print` just calls `std.io.console.
out`, and `std.read` just calls `std.io.console.in`.