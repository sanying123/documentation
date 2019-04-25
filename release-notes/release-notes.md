# ShiftLeft Release Notes

ShiftLeft Release Notes are updated every month for all products: ShiftLeft Ocular, ShiftLeft Inspect and ShiftLeft Protect. The following Release Notes are currently available:

* [April 2019](#april-2019-release-notes)
* [March 2019](#march-2019-release-notes)


## April 2019 Release Notes

* **Update to ShiftLeft's Terms of Service**. The ShiftLeft [Terms of Service](https://www.shiftleft.io/terms/) have been updated for post-termination obligations (4d). 

### ShiftLeft Ocular

* **New Tutorial on Creating a Code Property Graph (CPG) from a Java Archive (JAR)**. The ShiftLeft Ocular documentation now includes a [tutorial on creating a CPG from a JAR](../using-ocular/tutorials/cpgcreate.md). ShiftLeft Ocular creates a CPG for only the application code, with references to the dependency code. This distinction is made through the use of a built-in Smart Jar Unpacker, which heuristically determines for each namespace whether it contains application or dependency code.

#### ShiftLeft Ocular v0.3.23

* **New `Config` Objects for Specifying Custom Policy and Other Configurations**. The following new `config` objects have been introduced in ShiftLeft Ocular for specifying custom policy and other configurations:
  * `config.policy.dynamicPolicyPath("/path/to/dynamic/policy")`
  * `config.policy.staticPolicyPath("/path/to/dynamic/policy")`

* **The `workspaceReset` Command Replaced with `workspace.reset`**. The `workspaceReset` command has been deprecated and replaced with the `workspace.reset` command. The new command resets the workspace and deletes all CPGs stored on disk.

* **New `version` Command Added**. This new `version` command prints the current version string.

* **Determining Aliases**. ShiftLeft Ocular has been enhanced to allow determining aliases for a list of identifiers in C/C++ code.

#### ShiftLeft Ocular v0.3.20

* **On-Disk Graph Swapping for Low RAM Machines.** This experimental feature allows CPG elements to be swapped on disk as required from the main memory. Note that this feature adds extra latency of loading/unloading of memory and is not yet officially supported. Use the following function on the Ocular shell with either default parameters or custom ones to enable On-Disk Graph Swapping for Low RAM Machines: 
  * `enableOnDiskOverflow()`
  * `config.policy.staticPolicyPath("/path/to/dynamic/policy")`

* **Overlay API**. The Security Profile is now part of the CPG, as an overlay of the CPG. This new feature unifies the Ocular Query Language (OQL) for the CPG and Security Profile and removes the need for using `cpg2sp.sh` to create a Security Profile. From a fucntionality perspective, this means that all Security Profile functionality is now part of the CPG. For example, you now use `cpg.finding.p` instead of `sp.findings.p` The new Overlay feature requires that `cpg2sp` to be run with the --overlay flag. For ease of use, all of these steps have been integrated into ShiftLeft Ocular.

* **Integrated CPG and SP Generation**. CPG and Security Profile generation can now be performed from inside ShiftLeft Ocular, with CPGs along with their overlays managed in a “workspace”. This new feature allows you to effectively work with multiple CPGs at once.
  * `createCpg("/path/to/jar")`
  * `createCpgAndSp("/path/to/jar")`
  * `createSp(cpg)`

Older APIs and functionality (e.g. `loadCpg` and `loadSp`) are now backwards compatible.

* **Workspaces**. ShiftLeft Ocular now includes workspaces for easy management of CPGs and overlays. [Refer to the API] (https://ocular.shiftleft.io/api/io/shiftleft/repl/Console.html) for additional information.

* **Load Multiple CPG Queries**. You can load more than one CPG in a given workpace and then combine queries. For example `cpgs.flatMap(_.method.fullName.l)`

* **Load Multiple CPG Queries**. You can load more than one CPG in a given workpace and then combine queries. For example `cpgs.flatMap(_.method.fullName.l)`

* **Deprecated `sp` Object**. Functionality of the deprecated `sp` object has been transferred to `cpg` object.

* **Dependency List Outputs Complete Dependencies**. The Dependency List has been fixed to now output complete dependencies.

* **Rename newLocation Step**. The newLocation step has been rename to location.

* ** `.flows` Behavior Fixed**. `.flows` behavior has been fixed to show only single flow, thereby resolving printing issues. Use `.allFlows` to show the complete flows list.

------------------------------------------------

Ocular v0.3.17
Improve data flow tracking

------------------------------------------------

Ocular v0.3.10
Enhacements:
Faster data flow analysis engine with experimental security profile overlay features
Initial C/C++ and C# analysis support with fuzzyc2cpg.sh and csharp2cpg.sh
Allows data flow and code analysis from C/C++ and C# source code directly
Fixes:
Conclusions now populate properly on Security profile generation for some apps



### ShiftLeft Inspect and ShiftLeft Protect

* **Enhancements to ShiftLeft Inspect for .Net**. The current version of ShiftLeft Inspect for .Net includes significant performance improvements in both processing time and memory consumption. In addition, numerous bug fixes have been made.

* **JSP support added for ShiftLeft Inspect**. You can now use ShiftLeft Inspect to analyze your JSP pages for vulnerabilities and data leakage. Note that this support does not include JSP Expression Language.

* **Stability Improvements to ShiftLeft Protect**. Stability improvements have been made in the ShiftLeft Protect Microagent for Java.

* **Automatic Updates for the ShiftLeft Command Line Interface (CLI)**. The ShiftLeft CLI now automatically updates so that you don't have to reinstall the CLI whenever there are new features or fixes. Refer to [Using the CLI](../using-inspect-protect/using-cli/using-cli.md) for more information.


## March 2019 Release Notes

### ShiftLeft Inspect and ShiftLeft Protect

* **Vulnerability Dashboard**. The new Vulnerability Dashboard provides a singular view of application security quality metrics, including a list of vulnerabilities based on static/runtime analysis of applications. You can use these metrics to measure progress of your security improvement over time. [See the associated article](../using-inspect-protect/using-workflow/vulnerability-dashboard.md) for more information.

* **Jira Integration**. You can now integrate ShiftLeft with Jira to automatically generate Jira tickets for the vulnerabilities in your ShiftLeft Dashboard. Refer to the article [Enabling Jira Integration](../using-inspect-protect/using-workflow/jira-integration.md) for details.
