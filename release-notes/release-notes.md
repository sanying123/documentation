# ShiftLeft Release Notes

ShiftLeft Release Notes are updated every month for all products: ShiftLeft Ocular, ShiftLeft Inspect and ShiftLeft Protect. The following Release Notes are currently available:

* [April 2019](#april-2019-release-notes)
* [March 2019](#march-2019-release-notes)


## April 2019 Release Notes

* **Update to ShiftLeft's Terms of Service**. The ShiftLeft [Terms of Service](https://www.shiftleft.io/terms/) have been updated for post-termination obligations (4d). 

### ShiftLeft Ocular

* **New Tutorial on Creating a Code Property Graph (CPG) from a Java Archive (JAR)**. The ShiftLeft Ocular documentation now includes a [tutorial on creating a CPG from a JAR](../using-ocular/tutorials/cpgcreate.md). ShiftLeft Ocular creates a CPG for only the application code, with references to the dependency code. This distinction is made through the use of a built-in Smart Jar Unpacker, which heuristically determines for each namespace whether it contains application or dependency code.

### ShiftLeft Inspect and ShiftLeft Protect

* **Enhancements to ShiftLeft Inspect for .Net**. The current version of ShiftLeft Inspect for .Net includes significant performance improvements in both processing time and memory consumption. In addition, numerous bug fixes have been made.

* **JSP support added for ShiftLeft Inspect**. You can now use ShiftLeft Inspect to analyze your JSP pages for vulnerabilities and data leakage. Note that this support does not include JSP Expression Language.

* **Stability Improvements to ShiftLeft Protect**. Stability improvements have been made in the ShiftLeft Protect Microagent for Java.

* **Automatic Updates for the ShiftLeft Command Line Interface (CLI)**. The ShiftLeft CLI now automatically updates so that you don't have to reinstall the CLI whenever there are new features or fixes. Refer to [Using the CLI](../using-inspect-protect/using-cli/using-cli.md) for more information.


## March 2019 Release Notes

### ShiftLeft Inspect and ShiftLeft Protect

* **Vulnerability Dashboard**. The new Vulnerability Dashboard provides a singular view of application security quality metrics, including a list of vulnerabilities based on static/runtime analysis of applications. You can use these metrics to measure progress of your security improvement over time. [See the associated article](../using-inspect-protect/using-workflow/vulnerability-dashboard.md) for more information.

* **Jira Integration**. You can now integrate ShiftLeft with Jira to automatically generate Jira tickets for the vulnerabilities in your ShiftLeft Dashboard. Refer to the article [Enabling Jira Integration](../using-inspect-protect/using-workflow/jira-integration.md) for details.
