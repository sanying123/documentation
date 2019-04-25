## ShiftLeft Ocular

ShiftLeft Ocular is a set of command line tools that provide a static analysis framework in the context of security, and is aimed towards developers and security researchers interested in exploring code for vulnerabilities.

A [trial version (Java-only)](https://go.shiftleft.io/ocular-free-trial) with a limited feature set can be downloaded.

ShiftLeft Ocular provides the following core features:

* **Generation of [Code Property Graphs (CPG)](../introduction/products.md).** Based on your application code, which
  is provided as JAR for JAVA or as source code for C/C++, ShiftLeft Ocular generates a
  versatile, intermediate CPG. CPGs can be used as the basis of custom static analysis and are
  serializable to various output/exchange formats such as CSV, GraphML, Gryo,
  and Protobuf (included in the ShiftLeft Ocular trial version).

* **Interactive code analysis using a Read-Eval-Print-Loop (REPL).** CPGs can be interactively explored
  using a REPL, an interactive shell with support
  for [Ocular Query Language (OQL)](../introduction/products.md). Among other features, the REPL offers utilities
  for exporting security analysis results as plain text or in JSON format,
  readline support, and tab-completion (included in the ShiftLeft Ocular trial version).

* **Custom analysis scripts and extensibility.** User-provided REPL scripts can
  be executed non-interactively to perform automated custom scans for security
  issues. Moreover, you can even augment and customize OQL via the "pimp-my-library" pattern (included in the ShiftLeft Ocular trial version).

* **Framework and library support through policies.** ShiftLeft Inspect includes
  annotations for common Java frameworks and libraries. Possibly
  attacker-controlled data sources and interesting sinks are automatically tagged in the CPG, and flow descriptions exist to scan for common vulnerability
  patterns. You can provide additional annotations to extend supported
  frameworks and libraries or encode additional vulnerability patterns.

* **Automatic code scanning.** Policies can be applied to CPGs
  to generate *security profiles* which are summaries of
  vulnerabilities and data leaks present in the code. Similar to CPGs, security
  profiles can also be explored and processed using the REPL.


See Also
--------

* [ShiftLeft Ocular Demo by Fabian Yamaguchi](https://www.youtube.com/watch?v=n_dpgI2RhEU)
* [ShiftLeft Ocular Demo by Chetan Conikee](https://www.youtube.com/watch?v=bB2C-FzC1Yw)
