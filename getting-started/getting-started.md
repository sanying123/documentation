ShiftLeft is a cloud-based security service that analyzes your code, and then uses this analysis to monitor your application at runtime in production. 

In the analysis phase, ShiftLeft identifies your application's:
* attack surface
* inputs and outputs
* categories of data
* data flows
* weaknesses (such as mishandling attacker-controlled data or leaking sensitive variables in plain text)

The ShiftLeft Microagent, using the knowledge derived from the code analysis, runs alongside your application and enables runtime security monitoring. The Microagent is automatically customized to your application through the use of a Security Profile for Runtime (SPR), which informs the Microagent on how to instrument the application and how to monitor its specific shape and weaknesses. 

![ShiftLeft Workflow](shiftleft-workflow.jpg)

The combination of code analysis and runtime monitoring performed by ShiftLeft is what gives your application an edge over attackers, because the protection provided is very specific to the application.

> # Language Support
>
>Currently, ShiftLeft supports Java 7+ and C# 6.0. Support for other languages is in development. For inquiries, please fill out our [contact form](https://www.shiftleft.io/contact/).

# Requirements

To get started with ShiftLeft, you need:

* A ShiftLeft account ([contact us](https://www.shiftleft.io/contact/))
* Linux or Mac X OS (Windows support is experimental - please [use our installer](windows-installer.md))
* A Java application (or use [HelloShiftLeft](https://github.com/ShiftLeftSecurity/HelloShiftLeft))

# Downloading, Installing and Authenticating the ShiftLeft CLI

Once you have downloaded and installed the ShiftLeft CLI, verify the installation by typing `sl help`. See more information on [Using the ShiftLeft CLI](using-sl-the-shiftleft-cli.md).

## Linux

Download the [ShiftLeft CLI for Linux](https://cdn.shiftleft.io/download/sl-latest-linux-x64.tar.gz), or run the following command:

```bash
curl https://cdn.shiftleft.io/download/sl-latest-linux-x64.tar.gz | tar xvz -C /usr/local/bin
```

## Mac OS X

Download the [ShiftLeft CLI for Mac OS X](https://cdn.shiftleft.io/download/sl-latest-osx-x64.tar.gz), or run the following command:

```bash
curl https://cdn.shiftleft.io/download/sl-latest-osx-x64.tar.gz | tar xvz -C /usr/local/bin
```

## Windows .Net

Note that for Windows .NET there are two variants, either the .NET Framework or .NET Core version; be sure to pick the right one for your project.

After you have downloaded the appropriate installer, unzip the file and invoke the installer.  If you are running the installer from the terminal, add `--no-prompt` to disable waiting for user input.

### Windows .NET Framework

Download the [ShiftLeft Installer for Windows and .NET Framework](https://cdn.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip), or run the following command:

```bash
Invoke-WebRequest -Uri https://cdn.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

### Windows .NET Core

Download the [ShiftLeft Installer for Windows and .NET Core](https://cdn.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip), or run the following command:

```bash
Invoke-WebRequest -Uri https://cdn.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

## Authenticating the ShiftLeft CLI

Autheticating the ShiftLeft CLI stores the credentials to a local file. 

For Linux and Mac, run the following command:

```bash
sl auth
```

For Windows, run:

```bash
sl.exe auth
```

You are prompted for your Organization ID and Upload Token. This information is available from the [user profile page in the ShiftLeft dashboard](https://www.shiftleft.io/user/profile).
An alternative to authenticating the ShiftLeft CLI using the `sl auth` command is setting the environment variables `SHIFTLEFT_ORG_ID` and `SHIFTLEFT_UPLOAD_TOKEN`.
See [Authenticating with ShiftLeft](authenticating-with-shiftleft.md) for additional information.

# Running the ShiftLeft Microagent

Microagent support is currently only available for Java. Development is planned for .NET support; if you are interested in using the ShiftLeft Microagent for .NET, please fill out our [contact form](https://www.shiftleft.io/contact/).

## Running the Microagent for Java

In order to start your application with the Microagent, you need to prefix the command line you use to start your application with `sl run`.

For example, if your usual command is `java -jar target/hello-shiftleft-0.0.1.jar` and the packaged application is at `target/hello-shiftleft-0.0.1.jar`, then you can wrap the command as:

```bash
sl run \
  --app HelloShiftLeft \
  --analyze target/hello-shiftleft-0.0.1.jar \
  -- java -jar target/hello-shiftleft-0.0.1.jar
```

Where

* `--app <name>` specifies a unique name for the application.
* `--analyze <jar>` points the ShiftLeft CLI (i.e. `sl`) to the application's JAR to be analyzed before starting up.
* `--` delimits flags from the command to be wrapped. What comes after `--` is the command itself that is run with the installed Microagent.

The first time you run this command for a specific JAR, it takes a few minutes to perform the code analysis. Subsequent runs are faster. You also have the option of [pre-analyzing your applications](../getting-started/analyzing-applications-in-ci.md), so that starting up is always fast.

For more information, refer to [Installing the Microagent](../installing-the-microagent/installing-the-microagent.md) and  [Configuring the Microagent](../installing-the-microagent/jvm-based-environments/configuring-the-microagent.md).

#Triggering Activity in the Application

Once your application is running, you can trigger some activity or expose it to real traffic.

If you are using HelloShiftLeft, use the following script as an example:

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

Open the [ShiftLeft Dashboard](https://www.shiftleft.io/dashboard) to see activity.
