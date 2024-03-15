# 1.2. Build Tool

The build tool `S++` uses is called `spp`. It is a command line tool that can be used to compile and run S++ 
programs. The Intellij plugin will call the `spp` command line tool to compile and run S++ programs. The `spp` tool 
required the `build.toml` script, that is located in the root directory of the project, sibling to the `src` 
directory. The build script contains a simple set of rules for the `spp` tool to follow when compiling and running

## Build Script
### Project attributes: `[project]`
#### Core project attributes
The build script attributes are as follows:

| Attribute | Description                 | Type        |
|-----------|-----------------------------|-------------|
| `name`    | The name of the project.    | `str`       |
| `version` | The version of the project. | `str`       |
| `authors` | The authors of the project. | `list[str]` |

#### Additional project attributes

| Attribute     | Description                     | Type        | Default       |
|---------------|---------------------------------|-------------|---------------|
| `license`     | The license of the project.     | `str`       | `""`          |
| `readme`      | The readme file of the project. | `str`       | `"README.md"` |
| `description` | The description of the project. | `str`       | `""`          |
| `keywords`    | The keywords of the project.    | `list[str]` | `[]`          |

### VCS attributes: `[vcs]`
To include other projects that are on a VCS, the url of the repository is required. The repository is then checked 
for a `build.toml` file, which is verified to be valid. The project is then included in the build process. The type 
of VCS being used is detected from the URL, and the correct adapter is used to fetch the project.

#### Individual VCS attributes
| Attribute    | Description                                                                  | Type   | Default       |
|--------------|------------------------------------------------------------------------------|--------|---------------|
| `url`        | The URL of the repository.                                                   | `str`  | `N/A`         |
| `auto_fetch` | Whether to automatically fetch the project when there are updates available. | `bool` | `true`        |
| `branch`     | The branch of the project to use. Defaults to `master` or `main`.            | `str`  | `master/main` |

### Example build script
```toml
[project]
name = "My Project"
version = "0.1.0"
authors = ["SamG101"]

[vcs]
spp_compiler_4 = { url: "https://github.com/SamG101-Developer/SPP-Compiler-4" }
```

## Build Tool
The `spp` build tool has 6 commands, which are as follows:

#### `spp build`
- Standard build command for an s++ project (debug or release).
- Creates a `bin` directory next to the `src` directory.
- All binary/metadata files are placed in this `bin` directory.
- Does not run the binary after building.

| Flag             | Mutually Exclusive | Description                                |
|------------------|--------------------|--------------------------------------------|
| `-r`/`--release` | `-d`               | Build in release mode.                     |
| `-d`/`--debug`   | `-r`               | Build in debug mode.                       |
| `-c`/`--clean`   |                    | Clean the build directory before building. |
| `-h`/`--help`    |                    | Show help.                                 |


#### `spp run`
- Runs the binary files stored in the `bin` directory.
- The project must be built first: `spp run` does not build the project.
- No mode needs to be specified, as the binary files are already built.

| Flag          | Mutually Exclusive | Description |
|---------------|--------------------|-------------|
| `-h`/`--help` |                    | Show help.  |

#### `spp buildrun`
- Builds the project, then runs it.
- Calls `spp build [flags]`, then `spp run`.
- The flags are passed to `spp build`.

| Flag             | Mutually Exclusive | Description                                |
|------------------|--------------------|--------------------------------------------|
| `-r`/`--release` | `-d`               | Build in release mode.                     |
| `-d`/`--debug`   | `-r`               | Build in debug mode.                       |
| `-c`/`--clean`   |                    | Clean the build directory before building. |
| `-h`/`--help`    |                    | Show help.                                 |

#### `spp clean`
- Cleans the `bin` directory, but doesn't delete the folder.

| Flag          | Mutually Exclusive | Description |
|---------------|--------------------|-------------|
| `-h`/`--help` |                    | Show help.  |

#### `spp help`
- Shows help.
- Shows a list of commands, and their descriptions.

#### `spp version`
- Shows the version.
