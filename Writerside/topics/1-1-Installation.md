# 1.1. Installation

The "package" page contains the compiler downloads. The compiler is a single file executable, with downloads for
Windows, Linux, macOS, FreeBSD, Solaris and AIX, each automatically built per push to the `master` branch (in the
process of becoming the `main` branch).

PyInstaller will be used to convert the compiler into a standalone executable. The compiler will be installed under
the "spp" folder in the appropriate area, for example, under "Program Files" on Windows.

When the compiler is run for the first time, some environment variables will be set, allowing the compiler to be used
from the command line. The compiler is also the [build tool](1-2-Build-Tool.md), and handles the functionality of a
standard compiler and build tool.
