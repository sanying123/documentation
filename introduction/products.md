# ShiftLeft Products

ShiftLeft is a cloud-based security service with three products: 

* **ShiftLeft Inspect**. Anayzes your code.
* **ShiftLeft Protect**. Uses the analysis provided by ShiftLeft Inspect to monitor your application at runtime.
* **ShiftLeft Ocular**. Gives you a static analysis framework in the context of security.

During analysis, ShiftLeft Inspect identifies your application's:
* attack surface
* inputs and outputs
* categories of data
* data flows
* weaknesses (such as mishandling attacker-controlled data or leaking sensitive variables in plain text). 

Once code analysis is complete, ShiftLeft Protect automatically conducts runtime security monitoring of your application. This is done by deploying a ShiftLeft Microagent in-memory alongside your application in production. The Microagent is customized to your application's specific shape and weaknesses through the use of a Security Profile for Runtime (SPR).

Other components of the ShiftLeft Platform are:

* **ShiftLeft CLI**. The ShiftLeft command line interface (CLI) is used to submit applications for analysis and to run the ShiftLeft Microagent. 
* **ShiftLeft Dashboard**. Your visual interface with ShiftLeft Inspect and ShiftLeft Protect. Shows information on the security profiles of analyzed applications and monitoring the security of these applications in production.

![](../getting-started/shiftleft-workflow.jpg)

The combination of code analysis and runtime monitoring performed by ShiftLeft is what gives your application an edge over attackers, because the protection provided is very specific to your application.
