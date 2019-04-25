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

* **The `workspaceReset` Command Replaced with `workspace.reset`**. The `workspaceReset` command has been deprecated and replaced with the new `workspace.reset` command. The new command resets the workspace and deletes all CPGs stored on disk.

* **New `version` Command Added**. This new `version` command prints the current version string.

* **Determining Aliases**. ShiftLeft Ocular now allows determining aliases for a list of identifiers in C/C++ code.


Ocular v0.3.20
Experimental Features:
On-disk graph swapping for low RAM machines. This allows the CPG elements to be swapped on disk as required from the main memory. Note that this feature adds extra latency of loading/unloading of memory and is not officially supported yet.
For using this, you can use the following function on the Ocular shell with either default parameters or custom ones:
ocular> enableOnDiskOverflow()
ocular> enableOnDiskOverflow(cacheHeapPercentage = 30, storageDir = "/tmp")
New Features:
Overlay API. The security profile is now part of the code property graph. More specifically, it is an overlay of the code property graph. This unifies the query language for code property graph and security profile. this removes the need for using `cpg2sp.sh` for creating an SP. From a fucntionality perspective, all functionality of sp is now part of the cpg.
For example: cpg.finding.p instead of sp.findings.p
Overlays feature requires cpg2sp to be run with the --overlay flag. For ease of use we have integrated all these steps in Ocular itself.
Integrated CPG and SP generation: CPG and SP generation can now be performed from inside Ocular and CPGs along with their overlays are managed in a “workspace”. This allows to effectively work with multiple CPGs at once.
ocular> createCpg("/path/to/jar")
ocular> createCpgAndSp("/path/to/jar")
ocular> createSp(cpg)
Older APIs and functionality (loadCpg and loadSp) is backwards compatible
Workspaces: This version introduces workspaces which allows easy management of cpgs and overlays. For more info see API Docs: https://ocular.shiftleft.io/api/io/shiftleft/repl/Console.html
Multiple CPG Queries: You can load more than one CPG in a given workpace and then give combined queries. 
For example: ocular> cpgs.flatMap(_.method.fullName.l)
sp object deprecated. Functionality transferred to cpg object
Fixes:
Dependency list now outputs complete dependencies
Rename newLocation step to location
Fix .flows behavior to show only single flow to avoid printing issues .allFlows now shows complete flows list
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
