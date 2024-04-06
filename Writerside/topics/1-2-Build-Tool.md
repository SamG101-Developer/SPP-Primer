# 1.2. Build Tool

The build tool `S++` uses is the compiler itself: `spp`. It is a command line tool that can be used to compile and run
S++ programs. The Intellij plugin calls the `spp` command line tool to compile and run S++ programs. The `spp` tool
requires the `build.toml` script, which must be in the root directory of the project, sibling to the `src` directory.
The build script contains a simple set of rules for the `spp` tool to follow when compiling and running. If this file is
missing, then the compiler doesn't run.

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
of VCS being used is detected from the URL, and uses the correct adapter to fetch the project.

#### Individual VCS attributes

| Attribute    | Description                                                                  | Type     | Required | Default       |
|--------------|------------------------------------------------------------------------------|----------|----------|---------------|
| `url`        | The URL of the repository.                                                   | `string` | Y        | `N/A`         |
| `auto_fetch` | Whether to automatically fetch the project when there are updates available. | `bool`   | N        | `true`        |
| `branch`     | The branch of the project to use. Defaults to `master` or `main`.            | `string` | N        | `master/main` |

### Example build script

```
[project]
name = "My Project"
version = "0.1.0"
authors = ["SamG101"]

[vcs]
spp_compiler_4 = { url: "https://github.com/SamG101-Developer/SPP-Compiler-4" }
```

## Build Tool

The `spp` build tool has six commands, which are as follows:

#### `spp build`

- Standard build command for an S++ project (debug or release).
- The `bin` directory is created next to the `src` directory.
- All binary/metadata files are placed in the `bin` directory.
- The generated binary is **not** run automatically.

| Flag             | Mutually Exclusive | Description                                |
|------------------|--------------------|--------------------------------------------|
| `-r`/`--release` | `-d`               | Build in release mode.                     |
| `-d`/`--debug`   | `-r`               | Build in debug mode.                       |
| `-c`/`--clean`   |                    | Clean the build directory before building. |
| `-h`/`--help`    |                    | Show help for this command.                |

#### `spp run`

- The project must be built first: `spp run` does not build the project.
- The binary files stored in the `bin` directory are run.
- The specified mod is used when both the required and debug builds are present.

| Flag             | Mutually Exclusive | Description                  |
|------------------|--------------------|------------------------------|
| `-r`/`--release` | `-d`               | Runs the release mode build. |
| `-d`/`--debug`   | `-r`               | Runs the debug mode build.   |
| `-h`/`--help`    |                    | Show help for this command.  |

#### `spp buildrun`

- Combines the `build` and `run` commands.
- Calls `spp build [flags]`, then `spp run [flags]`.

| Flag             | Mutually Exclusive | Description                                |
|------------------|--------------------|--------------------------------------------|
| `-r`/`--release` | `-d`               | Build in release mode.                     |
| `-d`/`--debug`   | `-r`               | Build in debug mode.                       |
| `-c`/`--clean`   |                    | Clean the build directory before building. |
| `-h`/`--help`    |                    | Show help for this command.                |

#### `spp clean`

- The `bin` directory is emptied (both debug and release builds)

| Flag          | Mutually Exclusive | Description                 |
|---------------|--------------------|-----------------------------|
| `-h`/`--help` |                    | Show help for this command. |

#### `spp help`

- Shows help for the entire build tool.
- Shows a list of commands and their descriptions.

#### `spp version`

- Shows the version.
