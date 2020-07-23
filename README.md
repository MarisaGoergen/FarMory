# MORYX Template

[![Gitter](https://badges.gitter.im/MORYX-Industry/Development.svg)](https://gitter.im/MORYX-Industry/Development?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Recommended repository template for quickly starting the development of MORYX modules, plugins or entire applications. This template has the necessary package feeds, a back-end (*Application.sln*) and front-end (*Application.UI.sln*) solution, each with a launchable *StartProject*. The back-end solution is also pre-configured with the *Maintenance* module and graphic interface [MaintenanceWeb](https://github.com/PHOENIXCONTACT/MORYX-MaintenanceWeb), which you can use to interact with modules and change their configuration. The empty project *MyApplication* is your projects root namespace. It may contain facade, interface and domain model definitions. Remove it, if you do not need cross project type definitions.

## Getting Started

You can either use this repository as a template directly on GitHub or clone it like any other GIT repository. Afterwards just open the solutions and run the application. Per default this will require access to port 80, alternative you can configure a different port in the **WcfConfig* within the *StartProject*. While the server is running you can open the *MaintenanceWeb* at http://localhost/maintenanceweb/. The *Dashboard* gives you an overview of the application, *Modules* is used to interact and configure modules, *Models* lets you create databases and schemas for installed data models, while *Log* grants live access to all logs.

You can extend your solution by adding more packages to your *StartProject* or creating a MORYX package of your own. This repository includes [branches](#branches) with templates for common MORYX repositories. For details on different MORYX package types and documentation refer to the [MORYX-Platform](https://github.com/PHOENIXCONTACT/MORYX-Platform), [MORYX-CientFramework](https://github.com/PHOENIXCONTACT/MORYX-ClientFramework) and [MORYX-AbstractionLayer](https://github.com/PHOENIXCONTACT/MORYX-AbstractionLayer).

The projects, that you create yourself, need to be loaded in MORYX. Add a reference to your project in the *StartProject*. This will make sure, that your project is build every time you start debugging. It also ensures, that all your projects dependencies are present in the *StartProjects* execution directory and that the binary is removed on clean-up.

### Products Quick Start

The *ProductManager* needs a database for its *Moryx.Products.Model*. First make sure you have [PostgreSQL installed](https://www.postgresql.org/download/), then start the application and open [Database configuration](http://localhost/maintenanceweb/#/databases). Configure the *Moryx.Products.Model* and create the database. For details on product type definition and storage configuration, refer to the [documentation](https://github.com/PHOENIXCONTACT/MORYX-AbstractionLayer/blob/dev/docs/articles/Products/ProductDefinition.md).

Once you defined your product types and instances, configure the *ProductStorage*, either manually or by using the `AutoConfigurator` accessible through the *ProductManager* [console](http://localhost/maintenanceweb/#/modules/ProductManager/console). Once the module is running, start the front-end and you can create and configure products.

To access products outside the *ProductManager*, import the `IProductManagement` facade in your module and register it in the container.

## Branches

The *master* branch of this template is the bare minimum most developers will need to start, whether the build an application, a reusable module or a plugin to extend an existing module. There is a range of specialized branches for different use cases and tasks. Some branches include small class stubs, which you can either delete or adjust to your use case. You can start from a branch or merge it into *master*. With the merging technique you can also combine multiple templates by merging their branches into `master`. Below is a list of branches and their content:

- **master:** Base template with front- and back-end solution, *StartProject** and pre-installed *Maintenance* and *MaintenanceWeb*.
    - **[module](https://github.com/PHOENIXCONTACT/MORYX-Template/tree/module):** Empty module project with standard directory structure, *ModuleController*, *ModuleConfig* and *ModuleConsole*. 
    - **[al/resources](https://github.com/PHOENIXCONTACT/MORYX-Template/tree/al/resources):** Pre-installed *ResourceManagement* packages in front- and back-end, empty resource project, prepared configuration and setup instructions.
    - **[al/products](https://github.com/PHOENIXCONTACT/MORYX-Template/tree/al/products):** Pre-installed *ProductManagement* packages in front- and back-end, product definition stubs, prepared configuration and setup instructions.

**Note:** When you use this as a template on GitHub all branches are rewritten as initial commits and they lose their common ancestry, therefore can no longer be merged. The solution is to use `git replace --graft <template_branch> HEAD` from `master` **before** merging any branch. This will rewrite the commits parent and restore the lost ancestry. Afterwards you can use standard `git merge <template_branch>`. After assembling your initial template, remove all other branches for a clean repository.

## Inspirations

For inspiration, best practices and reusable packages, take a look at the MORYX based projects below. Open an issue or pull request, if you would like to add your project to the list.

- [HoMory](https://github.com/Toxantron/HoMory): MORYX based HomeAutomation example

## Trouble Shooting

If you run into problems with the template or MORYX development in general, feel free to join our Gitter channel, ask on StackOverflow using the [`moryx`](https://stackoverflow.com/questions/tagged/moryx) tag or open an issue. In case your back-end application closes directly after start, this is mostly caused by lack of rights, reserved ports or missing libraries. MORYX creates crash log before exiting which can be find in the subdirectory *CrashLogs* in the *StartProjects* execution directory.

## Contribute

If you have an idea to improve a template or can think of a new useful template, please make your changes based on one of the template branches and open a pull request. If you want to add a template, extend the branch list in one commit and the template definition in another. This way we can easily put your template into a separate branch. **Note:** All branches except *master* will be rebased and squashed regularly, to keep them clean. All merge requests that went into a template branch will combined in a single commit and its message appended with following merge request ids.  
