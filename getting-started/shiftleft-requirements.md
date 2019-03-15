# ShiftLeft Requirements

ShiftLeft runs as a [service](https://en.wikipedia.org/wiki/Software_as_a_service) with two integration points for your environment:

- ShiftLeft CLI to submit workloads for code analysis
- ShiftLeft Microagent for runtime monitoring

The ShiftLeft Dashboard provides the user interface for viewing the security profiles of analyzed applications and for monitoring the security of these applications in production.

## CLI Requirements

ShiftLeft provides the command line interface (CLI) tool named `sl` to submit applications for analysis and to run the ShiftLeft Microagent. The CLI requires a local installation of a supported Java version to download and run the ShiftLeft Analyzer Plugin. The CLI host must allow outbound connections on the specified port.

Component | Requirement
--- | ---
System | Linux, MacOS X, Windows
JVM | 64-bit **JRE** version **8** (Java 9 is not currently supported)

To verify that you are running the supported Java version, use the `java -version` command.

## Java Requirements for ShiftLeft Inspect

The ShiftLeft Inspect supports Java server applications built using one of the supported build tools listed below.

Component | Requirement
--- | ---
System | Linux, MacOS X, Windows
Application Type | **Java 8** or **Java 9**
Build environment | Linux or Mac with **Java 8** installed locally and with 16GB of memory available.

To verify that you are running the supported Java version, use the `java -version` command.

> #### Analysis requirements notes
>
> ShiftLeft code analysis is performed on compiled application bytecode (not source code). As such, you **must** successfully build the application using a supported build tool **before** you submit the app for analysis. See [Analyzing Applications](../getting-started/analyzing-applications-in-ci.md) for details.
>
> ShiftLeft requires the presence of a supported project build tool to generate security metadata from bytecode. The supported build tool must be installed on the host where you submit an application for analysis.
>
> Analysis should be performed for each code commit or build of the application. Automate analysis submissions using your preferred CI/CD system ([Bamboo](../integrating-with-shiftleft/integrating-bamboo-builds.md), CircleCI, [GoCD](../integrating-with-shiftleft/integrating-gocd-builds.md), [Jenkins](../integrating-with-shiftleft/integrating-jenkins-builds/integrating-jenkins-builds.md), [Travis](../integrating-with-shiftleft/integrating-travis-builds.md), [TeamCity](../integrating-with-shiftleft/integrating-teamcity-builds.md), etc.).

## Java Requirements for ShiftLeft Protect

The [ShiftLeft Microagent](../installing-the-microagent/installing-the-microagent.md) requires a supported 64-bit Java Runtime Environment (JRE). Each microagent runs in-memory within the same JVM as the deployed application. The microagent memory footprint is minimal (~50MB). 

Each Microagent connects to a ShiftLeft Proxy server to download the runtime security profile (SPR) and to send events and metrics to the ShiftLeft Dashboard. ShiftLeft hosts the proxy server, or we can provide an on-prem edition for supported platforms.

The microagent must be able to download data from and push metrics to the proxy server over the specified port. If using a firewall, open a connection to a remote service on the specified TCP port.

Component | Requirement
--- | ---
System | Linux, MacOS X, Windows
JVM | 64-bit **JRE** version **7** or higher

To verify that you are running a supported 64-bit JRE, use the `java -version` command.

## .NET Requirements for ShiftLeft Inspect

The analysis of .NET applications is supported for projects with the following characteristics.

Component | Target Type | Requirement
--- | --- | ---
Specification | | [MSBuild format](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild?view=vs-2017), *i.e.*, a .csproj file.
Language | | C# 7.0
Build environment | **.NET Framework** targets | MSBuild **15.0**. Visual Studio 2017 already comes with MSBuild 15.0. Otherwise, you can [download it from Microsoft](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=BuildTools&rel=15).
Build environment | **.NET Core** targets | .NET Core **2.1** or above.

To inspect which version of MSBuild is installed in your system, proceed as below:

1. In the Windows search bar, type *Developer Command Prompt for VS*.
2. Invoke MSBuild with the version flag: `msbuild /version`.

To verify whether a .NET Framework target can be built with MSBuild 15.0, proceed as below:

1. Open the *Developer Command Prompt for VS*.
2. Navigate to the project location.
3. Restore NuGet packages, if any: `nuget.exe restore MySolution.sln`.
3. Trigger a build: `msbuild MyProject.csproj` (applying additional options, if necessary).

> #### Analysis requirements notes
>
> As opposed to the scenario for Java, ShiftLeft code analysis for .NET is performed on **source code** (not on the equivalence of *byte code*, which is the [CIL](https://en.wikipedia.org/wiki/Common_Intermediate_Language)). In fact, our tooling does an actual build of the application. Therefore, the system where `sl` is run **must** must be able to successfully build the application. Remember to restore NuGet packages, if necessary.

## .NET Requirements for ShiftLeft Protect

Coming soon...

## Browser Requirements

ShiftLeft supports the following browsers for accessing, viewing, and interacting with the ShiftLeft Dashboard:

- Google Chrome (tested with v61, v62)
- Mozilla Firefox (tested with v57, v58b)
- macOS Safari (tested with v11)
- Microsoft Edge* (verified with v41)

NOTE: * Not officially supported currently, but generally should work with indicated version.
