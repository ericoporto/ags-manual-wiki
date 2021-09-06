# Script Modules

AGS script modules are a way for AGS script code to be reused and shared. They are written in AGS script code entirely, and thus are independent of the platform on which a game is run.

A Script Module is a pair of an AGS Script file and an AGS Script Header file, with an additional metadata.

## Managing modules

You can manage them by expanding the Script entry in the tree of Explore Project panel.

You can right click on Scripts to show options:
- **New script**
  - create a new module from scratch
- **Import script...**
  - load a module from a `.scm` file that you have downloaded
- **New folder**
  - creates folder, which can be used to organize script modules in groups

Right clicking on a folder of Script Modules should give the above options and additionally:
- **Move up**
  - The order of modules can be important, as it reflects the order in which they are compiled and run, so this option and the next let you change their ordering.
- **Move down**
  - moves the script module up in the order

Right clicking the module should give you the options:
- **Rename**
  - Give the module another name
- **Delete**
  - Removes an existing module from the game
- **Export...**
  - save your own module as a `.scm` file that you can share with others

## Writing Script Modules

When you click a module directly, you can use the properties panel to enter a brief
description of the module, a version number and authorship details in the module
manager when you create a module. Double clicking will expand and revel both the
script and the header files.

As when writing scripts, you need to reference a function that was previously
declared above, script modules should be ordered so that modules below only
reference functions that are import declared in the headers of the modules above
them in the Script listing in the Explore Project.

You can find useful script modules from others in the [Modules & Plugins board](https://www.adventuregamestudio.co.uk/forums/index.php?board=10.0) in the ags forums.

*See also:* [More on handling multiple scripts](MultipleScripts)
