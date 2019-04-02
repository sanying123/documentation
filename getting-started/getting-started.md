# Getting Started

ShiftLeft is a cloud-based security [service](https://en.wikipedia.org/wiki/Software_as_a_service) with two products that integrate with your environment: ShiftLeft Inspect and ShiftLeft Protect. ShiftLeft Inspect analyzes your code, and then ShiftLeft Protect uses this analysis to monitor your application at runtime. The ShiftLeft Dashboard is your visual interface with these products, providing information on the security profiles of analyzed applications and monitoring the security of these applications in production.

During analysis, ShiftLeft Inspect identifies your application's:
* attack surface
* inputs and outputs
* categories of data
* data flows
* weaknesses (such as mishandling attacker-controlled data or leaking sensitive variables in plain text). 

Once code analysis is complete, ShiftLeft Protect automatically conducts runtime security monitoring of your application. This is done by deploying a ShiftLeft Microagent in-memory alongside your application in production. The Microagent is customized to your application's specific shape and weaknesses through the use of a Security Profile for Runtime (SPR).

![](shiftleft-workflow.jpg)

The combination of code analysis and runtime monitoring performed by ShiftLeft is what gives your application an edge over attackers, because the protection provided is very specific to your application.

The process for getting started with ShiftLeft is:

1. [Download and install the ShiftLeft CLI](#downloading-and-installing-the-shiftleft-cli).
2. [Associatie the CLI with your ShiftLeft Account](#associating-the-cli-with-your-shiftleft-account).
3. [Run the ShiftLeft Microagent](#running-the-shiftleft-microagent).
4. [Trigger Activity in the Application](#triggering-activity-in-the-application).

## Language Support

Currently, ShiftLeft protects applications written in Java 7+ and C# 6.0. Support for other languages is in development. For inquiries, please fill out our [contact form](https://www.shiftleft.io/contact/).

## Requirements

To get started with ShiftLeft, you need:

* A ShiftLeft account ([contact us](https://www.shiftleft.io/contact/)).
* Linux, MacOS X or Windows .NET operating system. 
* A Java application you want to protect (or use the [HelloShiftLeft demo Java application](https://github.com/ShiftLeftSecurity/HelloShiftLeft)).

Make sure to refer to [ShiftLeft Requirements](shiftleft-requirements.md) for specifics on all requirements.

## Downloading and Installing the ShiftLeft CLI

The ShiftLeft command line interface (CLI) is used to submit applications for analysis and to run the ShiftLeft Microagent. The tool is named `sl`.

Once you have downloaded and installed the ShiftLeft CLI for your specific operating system, verify the installation by typing `sl help`. See more information on [Using the ShiftLeft CLI](using-sl-the-shiftleft-cli.md).

### Linux

Download the [ShiftLeft CLI for Linux](https://cdn.shiftleft.io/download/sl-latest-linux-x64.tar.gz), or run the following command:

```bash
curl https://cdn.shiftleft.io/download/sl-latest-linux-x64.tar.gz | tar xvz -C /usr/local/bin
```

### MacOS X

Download the [ShiftLeft CLI for MacOS X](https://cdn.shiftleft.io/download/sl-latest-osx-x64.tar.gz), or run the following command:

```bash
curl https://cdn.shiftleft.io/download/sl-latest-osx-x64.tar.gz | tar xvz -C /usr/local/bin
```

### Windows .Net

Note that for Windows .NET there are two variants, either the .NET Framework or .NET Core version; be sure to pick the right one for your project.

After you have downloaded the appropriate installer, unzip the file and invoke the installer.  If you are running the installer from the terminal, add `--no-prompt` to disable waiting for user input.

#### Windows .NET Framework

Download the [ShiftLeft CLI for Windows and .NET Framework](https://cdn.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip), or run the following command:

```bash
Invoke-WebRequest -Uri https://cdn.shiftleft.io/download/installer-dotnet-framework-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

#### Windows .NET Core

Download the [ShiftLeft CLI for Windows and .NET Core](https://cdn.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip), or run the following command:

```bash
Invoke-WebRequest -Uri https://cdn.shiftleft.io/download/installer-dotnet-core-latest-windows-x64.zip -UseBasicParsing -OutFile sl-latest-windows-x64.zip
```

## Associating the CLI with your ShiftLeft Account

To associate the CLI with your ShiftLeft account, copy and run the command provided in step 4 of your Welcome page.

![](WelcomeStep4.jpg)

## Running the ShiftLeft Microagent

Microagent support is available for Java and .NET.

### Running the Microagent for Java

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

## Triggering Activity in the Application

Once your application is running with the ShiftLeft Microagent, you can trigger some activity or expose it to real traffic. Then open the [ShiftLeft Dashboard](https://www.shiftleft.io/dashboard) to see that activity.

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

