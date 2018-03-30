## Maven Project Naming Conventions v1.0
Naming conventions are based on 
[Maven's Guide to naming conventions on groupId, artifactId and version](http://maven.apache.org/guides/mini/guide-naming-conventions.html)

When you create new maven module, there are entities that require consistent naming:
 * Folder structure that leads to module location
 * In pom.xml
    * `project.groupId`
    * `project.artifactId`
    * `project.name`
    * `project.version`

This small conventions set tries to simplify name generation, navigation and reduce char-noise.

### Leaf module folder name
 * Only lower case English letters and "-" sign are allowed.
 * Folder name must not duplicate information carried in the parent folders
 * Folder name must be singular

### project.groupId
Will identify your project uniquely across all projects, so we need to enforce a 
naming schema.
 * It has to follow the package name rules (see 
 [More information about package names](http://java.sun.com/docs/books/jls/third_edition/html/packages.html#7.7).)
 * Package name must be singular
 * Has to be at least as a domain name "**org.spacerace.mcb**" followed by 
 corresponding module set name.
 * A good way to determine the granularity of the `groupId` is to use the project 
 structure. That is, in a multiple module project, it should
append a new identifier to the parent's `groupId` eg.

        org.spacerace.mcb
        org.spacerace.mcb.webservice
        org.spacerace.mcb.webservice.chart
   This produces cleaner maven repository layout.

### project.artifactId
is the name of the jar without version
 * Only lower case English letters and "-" sign are allowed.
 * Must uniquely identify the artifact when resulting jars end-up in libraries 
 (since artifact ID by default is the same as resulting jar name). So artifact id
 is constructed based on folder structure.

        <project-name>-<top-level-module-name>-<sub-module-name>-...-<leaf-module-name>-<ending>
    for MCB project always =`mcb`. E.g. `mcb-webservice-chart-aggregator-parent`

Based on module's type, artifact name might be appended with special ending.

| Ending             | Usage case                                                    |
| ------------------ | ------------------------------------------------------------- |
|`-parent`           | If this POM file is specified as "parent" in any other module |
|`-aggregator`       | If it's an aggregating project (builds several sub-projects)  |
|`-aggregator-parent`| If module is both aggregator and parent.                      |
|--                  | No suffix for all other kinds of modules                      |


### project.name
Name is a more literate view of atrifact ID and is helpful during project build to 
distinguish which module is currently built.
 * Allows upper/lower case English letters, white-spaces and "-" sign.</li>
 * Words start with upper-case letter</li>
 * It's being constructed as

        MCB - <top-level-module-name> - <sub-module-name> - ... - <leaf-module-name>
    e.g. `MCB - Webservice - Chart - Service`

Project name might also be used by IDEs (like e.g. IntelliJ IDEA) to display your maven modules. So 
One'd want this uniform and properly ordered.

### project.version
This conventions set will not cover versioning. Instead it refers to most common one: 
[The Semantic Versioning](https://semver.org/)

### project.description
While optional, still recommended to add a good description to module general 
purpose and responsibilities.

## Samples
Table below illustrates the rules

<table>
    <tbody>
        <tr>
            <th>Directory Structure</th>
            <th>Group ID</th>
            <th>Artifact ID</th>
            <th>Name</th>
        </tr>
        <tr>
            <td>
<pre>
mcb
 ├─ parent-pom
 │  ...
 ├─ portlet
 │   ├─ life-support
 │   ├─ power-supply
 │   │  ...
 │   ├─ propulsion-stage-one
 │   └─ propulsion-stage-two
 │  ...
 ├─ set-up
 │   └─ local-libraries
 └─ webservice
     ├─ chart
     │   ├─ client
     │   ├─ service
     │   └─ web
     │  ...
     └─ workflow
         ├─ client
         ├─ service
         └─ web
</pre>
            </td>
            <td>
<pre>
org.spacerace.mcb
org.spacerace.mcb
  ...
org.spacerace.mcb.portlet
org.spacerace.mcb.portlet
org.spacerace.mcb.portlet
  ...
org.spacerace.mcb.portlet
org.spacerace.mcb.portlet
  ...
&nbsp;
org.spacerace.mcb.setup
org.spacerace.mcb.webservice
org.spacerace.mcb.webservice.chart
org.spacerace.mcb.webservice.chart
org.spacerace.mcb.webservice.chart
org.spacerace.mcb.webservice.chart
  ...
org.spacerace.mcb.webservice.workflow
org.spacerace.mcb.webservice.workflow
org.spacerace.mcb.webservice.workflow
org.spacerace.mcb.webservice.workflow
</pre>
            </td>
            <td>
<pre>
mcb-aggregator
mcb-parent
  ...
mcb-portlet-aggregator-parent
mcb-portlet-life-support
mcb-portlet-power-supply
  ...
mcb-portlet-propulsion-stage-one
mcb-portlet-propulsion-stage-two
  ...
&nbsp;
mcb-setup-local-libraries
mcb-webservice-aggregator-parent
mcb-webservice-chart-aggregator-parent
mcb-webservice-chart-client
mcb-webservice-chart-service
mcb-webservice-chart-web
  ...
mcb-webservice-workflow-aggregator-parent
mcb-webservice-workflow-client
mcb-webservice-workflow-service
mcb-webservice-workflow-web
</pre>
            </td>
            <td>
<pre>
MCB - Aggregator
MCB - Parent
  ...
MCB - Portlet - Aggregator Parent
MCB - Portlet - Life Support
MCB - Portlet - Power Supply
  ...
MCB - Portlet - Propulsion Stage One
MCB - Portlet - Propulsion Stage Two
  ...
&nbsp;
MCB - Set Up - Local Libraries
MCB - Web Service - Aggregator Parent
MCB - Web Service - Chart - Aggregator Parent
MCB - Web Service - Chart - Client
MCB - Web Service - Chart - Service
MCB - Web Service - Chart - Web
  ...
MCB - Web Service - Workflow - Aggregator Parent
MCB - Web Service - Workflow - Client
MCB - Web Service - Workflow - Service
MCB - Web Service - Workflow - Web
</pre>
            </td>
        </tr>
    </tbody>
</table>

