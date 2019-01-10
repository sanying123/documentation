# Using sl - the ShiftLeft CLI

The ShiftLeft command line Interface (CLI) is used to:
- [Authenticate with ShiftLeft](doc:auth) and associate your applications with the organization you are in.
- [Submit applications for analysis and profiling](doc:analyze) to the ShiftLeft service. 
- [Run the ShiftLeft Microagent](doc:run) with analyzed applications for runtime monitoring and metrics.

## Requirements

Refer to the [CLI Requirements](doc:requirements#section-cli-requirements) for details.

## Installation on Linux

To install the ShiftLeft CLI on Linux:
1. Make sure that `/usr/local/bin` is in your `$PATH`.
2. Run the following shell command as root.
3. Run `sl help` to verify installation.

```bash
curl https://www.shiftleft.io/download/sl-latest-linux-x64.tar.gz | tar xvz -C /usr/local/bin
```

## Installation on MacOS

To install the ShiftLeft CLI on MacOS X:
1. Make sure that `/usr/local/bin` is in your `$PATH`.
2. Run the following shell command as root.
3. Run `sl help` to verify installation.

```bash
curl https://www.shiftleft.io/download/sl-latest-osx-x64.tar.gz | tar xvz -C /usr/local/bin
```

## Installation on Windows

To install the ShiftLeft CLI on Windows, please refer [to our installer page](doc:windows-installer).

## Manual Installation

To manually install the ShiftLeft CLI:
* Download the release for your platform:
  * Linux: [sl-latest-linux-x64.tar.gz](https://www.shiftleft.io/download/sl-latest-linux-x64.tar.gz)
  * MacOSX: [sl-latest-osx-x64.tar.gz](https://www.shiftleft.io/download/sl-latest-osx-x64.tar.gz)
  * Windows: [sl-latest-windows-x64.zip](https://www.shiftleft.io/download/sl-latest-windows-x64.zip)
* Extract the `sl`/`sl.exe` binary from the file you just downloaded.
* Add the directory location of the `sl` binary to your `$PATH` (or manually copy it to `/usr/local/bin`).
* Run `sl help`/`sl.exe help` to verify installation.

## CLI Usage

The ShiftLeft CLI is invoked using the following syntax:

```
sl [global options] command [command options] [arguments...]
```

### `sl` commands

Command | Description
--- | ---
`auth` | [Authenticate](doc:auth) using `organization ID` and `upload token`.
`analyze [<path>]` | Submit application for [analysis](doc:analyze). If `<path>` is not provided, then `.` is implied. `<path>` can be the path to a `.jar`, `.war` or `.ear` file, or it can be the path to a Java project directory.
`run -- <command>` | Run target command with the [ShiftLeft Microagent](doc:run).
`push <path> [<path>...]` | Upload policies to ShiftLeft (coming soon).
`update [java-agent|libplugin]` | Update certain component of `sl`. Use `sl update java-agent` to auto-update the ShiftLeft Java Microagent.
`install [dotnet-agent]` | Runs the ShiftLeft .NET Microagent installer.
`help`, `h` | List `sl` commands or help for one command.

### `sl` global options

Global Option | Environment Variable | Description
--- | --- | ---
`--verbose` | `SHIFTLEFT_VERBOSE=true` | Verbose mode.
`--sl-home <path>` | `SHIFTLEFT_HOME=<path>` | Path for config files and artifacts. If `$HOME` is set, defaults to `$HOME/.shiftleft`, otherwise to `/etc/shiftleft`.
`--help`, `-h` | | Display `sl` help text.
`--version`, `-v` | | Display the `sl` version.
None | `https_proxy=<proxy>` | Proxy configuration.

### `sl analyze` options

`sl analyze` option | Environment Variable | Description
--- | --- | ---
`--cpg` | `SHIFTLEFT_CPG=true` | Submit application for analysis using [CPG mode](doc:analyze#section-sl-analyze-cpg).
`--app <name>`, `-a <name>` | `SHIFTLEFT_APP=<name>` | Associate analysis with this application name. This name will be used in the ShiftLeft UI.
`--wait`, `-w` | `SHIFTLEFT_WAIT=true` | Wait for analysis to finish before returning control.
`--java` | `SHIFTLEFT_LANG_JAVA=true` | Analyze Java code (implicit).
`--csharp` | `SHIFTLEFT_LANG_CSHARP=true` | Analyze C# code. 
`--estimate` | | Produce an estimate of the number of statements of the analyzed code. Requires `--cpg` to be set. (Only valid for Java.)
`--force` | | Force analysis (instead of using a cached result).
`--dotnet-core` | | Uses .NET Core. (Only valid for C#.)
`--dotnet-framework` | | Uses .NET Framework. (Only valid for C#.)
`--shiftleft-json-file` | `SHIFTLEFT_JSON_FILE=<path>` | Path to agent configuration file `shiftleft.json`. Defaults to `shiftleft.json` (in the current working directory).

### `sl run` options

`sl run` option | Environment Variable | Description
--- | --- | ---
`--analyze <file.jar>` | `SHIFTLEFT_ANALYZE=<file.jar>` | Perform analysis before running the application. If analysis has previously been performed on this version of this application, then no further analysis is performed and the application is started immediately.
`--app <name>`, `-a <name>` | `SHIFTLEFT_APP=<name>` | Associate analysis with this application name. This name will be used in the ShiftLeft UI. Only used when `--analyze` is passed.
`--cpg` | `SHIFTLEFT_CPG=true` | Submit application for analysis using [CPG mode](doc:analyze#section-sl-analyze-cpg). Only used when `--analyze` is passed.
`--java` | `SHIFTLEFT_JAVA=true` | This is a Java application (implicit).
None | `SHIFTLEFT_CONFIG=<path> ` | Path to the `shiftleft.json` file. Defaults to `./shiftleft.json`.

### `sl install` options

`sl run` option | Description
--- | ---
`--dotnet-core` | Uses .NET Core.
`--dotnet-framework` | Uses .NET Framework.

### Artifacts stored by `sl`

Artifact  | Description
--- | ---
`./shiftleft.json` | Analyzer output storing information necessary for running the ShiftLeft Microagent. This is used to correctly associate the analysis with the specific application version that will be run.
`$SHIFTLEFT_HOME/config.json` | Credentials file generated on successful authentication.
`$SHIFTLEFT_HOME/libplugin-a.b.c.jar` | ShiftLeft Analyzer Plugin downloaded or updated during analysis.
`$SHIFTLEFT_HOME/libplugin-latest.jar` | Symlink to the latest downloaded ShiftLeft Analyzer Plugin.
`$SHIFTLEFT_HOME/sl-microagent-x.y.z.jar` | ShiftLeft Microagent downloaded.
`$SHIFTLEFT_HOME/sl-microagent-latest.jar` | Symlink to the latest downloaded ShiftLeft Microagent.
