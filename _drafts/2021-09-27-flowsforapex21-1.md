---
title: "What's new in Flows for APEX 21.1"
last_modified_at: 2021-09-27T10:00:00+02:00
toc: true
categories:
  - Oracle APEX
  - Flows for APEX
tags:
  - workflow
  - APEX
  - bpmn
---

Flows for APEX 21.1 was released on Friday 24 September, now it's time to see what the main changes and new features of this major release are. If you want to see the complete list, you can can find it <a href="https://github.com/mt-ag/apex-flowsforapex/blob/v21.1/changelog.md">there</a>.
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Here it is: Flows for APEX 21.1! Thanks to <a href="https://twitter.com/commi235">@commi235</a> <a href="https://twitter.com/FlowquestR">@FlowquestR</a> <a href="https://twitter.com/moreaux_louis">@moreaux_louis</a> <a href="https://twitter.com/dennisamthor">@dennisamthor</a> as well as our beta testers for making this possible. <a href="flowsforapex.mt-ag.com">flowsforapex.mt-ag.com</a></p>&mdash; Niels de Brujin (@nielsdb) <a href="https://twitter.com/nielsdb/status/1441368868614664194">September 24, 2021</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

#### Introducing variable expressions
Previously, to set process variables you have to use the PL/SQL api or the process plug-ins. Starting from 21.1, you can use the new variable expressions feature. 
Just click on an activity in the modeler and on the property pannel, a new tab allows you to define the variable expression.

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/varExpression.apng){: .align-center}

Variable expression can be define using:
- Static value
- Process variable value
- SQL query returning one value
- SQL query returning multiple values (colon separated)
- PL/SQL expression
- PL/SQL function body

A typical use case is to use these expressions to define gateway route by using database values.

#### Better error handling 
A big change in this version is that the transaction system have been completely rewritten. The result of that is now each step of a process use a separate database transaction. The main addition is the error handling, the engine is now able to catch errors on the step, log them and put the step and the process instance in error status. 

![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/errorHandling.apng){: .align-center}

#### Process plug-ins
In version 5.1.2, we started to develop process plug-ins to make the integration of Flows for APEX in your applications easier. In this release, 3 new plug-ins are part of the distribution:
- Manage Flow Instance
- Manage Flow Instance Step
- Manage Flow Instance Variables

#### Modeler enhancements
The BPMN modeler have been improved by adding keyboard shorcut and the property panel is now expandable.
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/keyboardShortcuts.apng){: .align-center}

#### Multiple models export/import
A feature designed to make your models deployments easier is the 1-click export/import. On the Flow Management page, select the models to be exported and then use the header menu and choose Export. You can then choose between exporting to BPMN or SQL scripts. The result of this export is a zip archive containing the selected flows. For the SQL script version, you will only have to execute the import.sql script to perform the import. The BPMN version allows you to retrieve all the diagrams in BPMN format as well as an import.json file containing the attributes of each model (name, version, category). This archive can be used in the import dialog to import all the models in one click, just choose the Multiple models option.