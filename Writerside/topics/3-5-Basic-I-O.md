# 3.5. Basic I/O

IO is split into a few major categories: file IO, console IO, and network IO. Each set of IO has its own namespaced 
functions, but there are some aliases to make it easier to use. For example, `std.print` calls `std.io.console.out`,
and `std.read` just calls `std.io.console.in`.

## Console IO


## File IO
The FileIO revolves around the `std.io.File` class:

```s++
use U8 as FileMode

cls File {
    path: Str;
    mode: FileMode;
}

sup File {
    fun open(path: Str, mode: FileMode) -> Ret[File, FileNotFoundErr] {
        ##
        Open the file at the specified path with the specified mode. The mode
        dictates the permissions of the file, and whether it is opened for
        reading, writing, or both. If the file is not found, a FileNotFoundErr
        is returned.
        ##
    }
    
    fun read(&self, size: USize) -> Ret[Str, FilePermissionErr | FileReadErr] {
        ##
        Read the specified number of bytes from the file, into a string. If the
        file doesn't have the read permission, a FilePermissionErr is returned.
        If the file cannot be read from, a FileReadErr is returned.
        ##
    }
    
    fun write(&self, data: Str) -> Ret[Void, FilePermissionErr | FileWriteErr] {
        ##
        Write the specified string to the file. If the file doesn't have the
        write permission, a FilePermissionErr is returned. If the file cannot be
        written to, a FileWriteErr is returned.
        ##
    }
    
    fun append(&self, data: Str) -> Ret[Void, FilePermissionErr | FileWriteErr] {
        ##
        Append the specified string to the file. If the file doesn't have the
        write permission, a FilePermissionErr is returned. If the file cannot be
        written to, a FileWriteErr is returned.
        ##
    }
    
    fun close() -> Ret[Void, FileCloseErr] {
        ##
        Close the file. If the file cannot be closed, a FileCloseErr is
        returned.
        ##
    }
}
```

The file class is known to the compiler, as i

## Network IO
