# Creating a Code Property Graph (CPG) from a Java Archive

Java applications are distributed in Java Archives (JARs) and Web Application Archives (WARs). These archives contain both the application code and code for all dependencies.

Generally, you use ShiftLeft Ocular to analyze your application code and determine vulnerable dependencies. As part of this process, ShiftLeft Ocular creates a CPG for only the application code, and with references to the dependency code. ShiftLeft Ocular makes this distinction through the use of a built-in Smart Jar Unpacker, which heuristically determines for each namespace whether it contains application or dependency code.

For example, for the demo Java application `hello-shiftleft`, you create the CPG by running the command

```
createCpg("hello-shiftleft-0.0.1-SNAPSHOT.jar")
```

Your application's namespaces can then be viewed using the following query

```
cpg.namespace.internal.l
```

Dependency namespaces can be viewed with the query

```
cpg.namespace.external.l
```

You can also determine, prior to creating the CPG, which packages the Smart Jar Unpacker treats as application packages. To view application namespaces, use the query

```
appNamespaces("subjects/hello-shiftleft-0.0.1-SNAPSHOT.jar")
```

and to view dependency namespaces, use

```
depNamespaces("subjects/hello-shiftleft-0.0.1-SNAPSHOT.jar")
```

If you want to manually choose application namespaces for CPG creation, you can pass those namespaces to the `createCpg` command. For example, to specify explicitly that the application namespace is `io.shiftleft`, you would use the command

```
createCpg("subjects/hello-shiftleft-0.0.1-SNAPSHOT.jar", List("io.shiftleft"))
```
