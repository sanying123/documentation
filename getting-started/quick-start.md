# Quick Start

ShiftLeft is a cloud-based security service that monitors your application in production, based on a runtime agent. The runtime agent's configuration is custom to the version of the application that you protect, as it is informed by code analysis.

Behind the scenes, ShiftLeft works in two steps:

* Analysis
* Monitoring in runtime

In its analysis step, ShiftLeft identifies the application's attack surface, its inputs, outputs, categories of data handled, the way the data flows throughout the application and any weaknesses the application might have - like mishandling attacker-controlled data or leaking sensitive variables in plain text.

Informed by the knowledge derived from code analysis, a custom instrumentation called Security Profile for Runtime (SPR) is created and loaded onto a ShiftLeft microagent that runs alongside the application. This informs the microagent on how to instrument the application and how to monitor its specific shape and weaknesses.

![ShiftLeft Workflow](shiftleft-workflow.jpg)

The combination of code analysis and runtime monitoring is what gives the application an edge over attackers as the protection provided is very specific to the application itself.

## Getting Started

> #### Language Support
>
> For now, ShiftLeft supports Java 7+ and C# 6.0. Other languages are coming soon. For inquiries, please fill out our [contact form](https://www.shiftleft.io/contact/).

To get started, you will need 

* A ShiftLeft account ([contact us](https://www.shiftleft.io/contact/))
* Linux or Mac OS X (Windows support is experimental - please [use our installer](doc:windows-installer))
* A Java application (or use [HelloShiftLeft](https://github.com/ShiftLeftSecurity/HelloShiftLeft))

### Step 1: Download and Install sl - the ShiftLeft CLI

#### Linux

```bash
curl https://www.shiftleft.io/download/sl-latest-linux-x64.tar.gz | tar xvz -C /usr/local/bin
```

#### Mac OS X

```bash
curl https://www.shiftleft.io/download/sl-latest-osx-x64.tar.gz | tar xvz -C /usr/local/bin
```

#### Windows .NET Framework

```bash
Invoke-WebRequest -Uri https://www.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

#### Windows .NET Core

```bash
Invoke-WebRequest -Uri https://www.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

#### Or download and install manually

  * [sl for Linux](https://www.shiftleft.io/download/sl-latest-linux-x64.tar.gz)
  * [sl for Mac OS X](https://www.shiftleft.io/download/sl-latest-osx-x64.tar.gz)
  * [sl for Windows .NET Framework](https://www.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip)
  * [sl for Windows .NET Core](https://www.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip)

Verify that the installation worked by typing `sl help`. See more information about sl on the [Using the ShiftLeft CLI](doc:cli) page.

### Step 2: Authenticate sl

```bash
sl auth
```

or on Windows

```bash
sl.exe auth
```

* This will prompt for your Organization ID and your Upload Token. You will find this information on the [user profile page in the ShiftLeft dashboard](https://www.shiftleft.io/user/profile)
* An alternative to using `sl auth` (which stores the credentials to a local file) is setting the environment variables `SHIFTLEFT_ORG_ID` and `SHIFTLEFT_UPLOAD_TOKEN`
* See more information about authentication on the [Authenticating with ShiftLeft](doc:auth) page

### Step 3: Run with Microagent

> #### Microagent support
>
> The instructions below apply to Java only. Microagent support for .NET is coming soon. For inquiries, please fill out our [contact form](https://www.shiftleft.io/contact/).

In order to start your application with the ShiftLeft Microagent, you need to prefix the command line you use to start your application with `sl run`.

For example, if your usual command is `java -jar target/hello-shiftleft-0.0.1.jar` and the packaged application is at `target/hello-shiftleft-0.0.1.jar`, then you can wrap the command like so:

```bash
sl run \
  --app HelloShiftLeft \
  --analyze target/hello-shiftleft-0.0.1.jar \
  -- java -jar target/hello-shiftleft-0.0.1.jar
```

* `--app <name>` specifies a unique name for the application
* `--analyze <jar>` points `sl` to the application's JAR to be analyzed before starting up
* `--` delimits flags from the command to be wrapped. What comes after `--` is the command itself that will be run with the ShiftLeft Microagent installed

The first time you run this command for a specific JAR, it will take a few minutes to perform the analysis. Subsequent runs will be fast. You also have the option of [pre-analyzing applications](doc:analyze) so that starting up is always fast.

See more information about installing the Microagent on the [Installing the Microagent](doc:run) page or the [Configuring the Microagent](doc:microagent) page.

### Step 4: Trigger activity in the application

Once the application is running, you can trigger some activity in your application or expose it to real traffic.

If you are using HelloShiftLeft, you can use the following script as an example:

```bash
while true ; do \
curl -s localhost:8081/customers/2 >/dev/null ;\
curl -s localhost:8081/customers/1 >/dev/null ;\
sleep 1 ;\
curl -s localhost:8081/customers/2 >/dev/null ;\
curl -s localhost:8081/customers/1 >/dev/null ;\
sleep 1 ;\
curl -s localhost:8081/customers/1 >/dev/null ;\
curl -s localhost:8081/customers/1 >/dev/null ;\
sleep 1 ;\
curl -s localhost:8081/customers >/dev/null ;\
curl -s localhost:8081/saveSettings >/dev/null ;\
sleep 1 ;\
curl -s localhost:8081/customers >/dev/null ;\
sleep 1 ;\
curl -s localhost:8081/ >/dev/null ;\
curl -s localhost:8081/account/1 >/dev/null ;\
curl -s localhost:8081/account >/dev/null ;\
curl -s localhost:8081/account/2 >/dev/null ;\
curl -s localhost:8081/account >/dev/null ;\
curl -s localhost:8081/account/3 >/dev/null ;\
curl -s localhost:8081/account/3 >/dev/null ;\
curl -s localhost:8081/account/4 >/dev/null ;\
curl -s localhost:8081/account/5 >/dev/null ;\
curl -s localhost:8081/account/5 >/dev/null ;\
curl -s localhost:8081/account/5 >/dev/null ;\
curl -s localhost:8081/off >/dev/null ;\
sleep 1 ;\
done
```

Open [the ShiftLeft Dashboard](https://www.shiftleft.io/dashboard) to see activity.
